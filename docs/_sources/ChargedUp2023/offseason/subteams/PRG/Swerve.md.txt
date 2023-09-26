### Overview

Last year, our swerve drive code was written really badly, and had lots of issues.

One of the largest issues that prevented us from making proper autos was the orientation of our swerve drive.
Our old swerve drive code followed the North, East, Up convention, which can be seen below:

![Old Swerve Orientation](PRG/images/Swerve-NEU.png)

This can be seen in our code:
```java
public static final SwerveDriveKinematics kDriveKinematics = new SwerveDriveKinematics(
      new Translation2d(kWheelBase / 2, -kTrackWidth / 2),  // Front Left (x, -y)
      new Translation2d(kWheelBase / 2, kTrackWidth / 2),   // Front Right (x, y)
      new Translation2d(-kWheelBase / 2, -kTrackWidth / 2), // Back Left (-x, -y)
      new Translation2d(-kWheelBase / 2, kTrackWidth / 2)); // Back Right (-x, y)
```

However, the [swerve drive kinematics](https://docs.wpilib.org/en/stable/docs/software/kinematics-and-odometry/swerve-drive-kinematics.html) class in WPILib actually follows the North, West, Up convention:

![Real Swerve Orientation](PRG/images/Swerve-NWU.png)

This should have caused all of our wheels to become flipped horizontally (across the x-axis), as the front right module was being treated like the back right module and vice versa. This would make the swerve drive undrivable, as when rotating, it would cause the modules to get stuck in an "X" shape.

However, we made another mistake that perfectly cancelled this out.

Because of the way Falcon 500 motors are mounted in Mk4i Swerve Modules, a clockwise rotation in the falcon 500 results in a clockwise rotation of the entire swerve module:

![Swerve Module Orientation](PRG/images/SwerveModule.png)

Because we didn't invert our Falcons, this "un-flipped" the reversed module rotations. 

However, this would cause the CANCoders in our modules to read different angles due to reading as Counter-Clockwise positive, causing us to invert our CANCoders.

We can see the impact of these messed-up coordinate conventions in our code. For example, our module "tow" states, which is where all of the swerve modules turn inwards to lock the entire drivetrain in place, has clockwise-positive angles, instead of counterclockwise-positive angles.

```java
public static final SwerveModuleState[] towModuleStates = 
    new SwerveModuleState[] {
        new SwerveModuleState(0.01, Rotation2d.fromDegrees(45)),  // Front Left
        new SwerveModuleState(0.01, Rotation2d.fromDegrees(135)), // Front Right
        new SwerveModuleState(0.01, Rotation2d.fromDegrees(-45)), // Back Left
        new SwerveModuleState(0.01, Rotation2d.fromDegrees(-135)) // Back Right
    };
```

### Fixing the Problem

By the time we realized this problem during the 2023 season, it was too late for us to change our swerve drive code, as we were already mid-season and didn't want to spend our testing time fixing this problem. This ended up being a bad decision, as it stopped us from making any complex autos, and caused weird behavior when moving backwards in autos.

As a result, as soon as offseason started, the very first thing we did was create a fork of our ChargedUp2023 code called [SwerveDrive2023](https://github.com/nerdherd/SwerveDrive2023), where we would fix these issues and make a reusable swerve drive template for ourselves.

To fix our issues, we implemented the following changes:
1. Switch to North-West-Up conventions in our Swerve Drive Kinematics class
2. Invert our Falcon 500s
3. Un-invert our CANCoders
4. Modify hard-coded states

Implementing these changes solved our issues with a flipped drivebase, and allowed us to properly use autonomous trajectory libraries such as PathPlanner. You can read more about how we used PathPlanner in the [Autos](#autos) section.

### State Control

One issue with our past implementation of our Swerve Drive came from how the modules were controlled.

In our original code, we set the desired state of each module and controlled the modules to move towards the state in the same method, setDesiredState:

```java
/**
 * Set the desired state of the Swerve Module and move towards it
 * @param state The desired state for this Swerve Module
 */
public void setDesiredState(SwerveModuleState state) {
    if (Math.abs(state.speedMetersPerSecond) < 0.001) {
        stop();
        return;
    }
    state = SwerveModuleState.optimize(state, getState().angle);

    desiredAngle = state.angle.getDegrees();
    
    currentPercent = state.speedMetersPerSecond / SwerveDriveConstants.kPhysicalMaxSpeedMetersPerSecond;
    driveMotor.set(ControlMode.PercentOutput, currentPercent);
    
    double turnPower = turningController.calculate(getTurningPosition(), state.angle.getRadians());
    turnMotor.set(ControlMode.PercentOutput, turnPower);
}
```

Although this works for teleoperated input, as the drive command will constantly be sending new states to the swerve modules, one issue comes from autos. 

At the end of our dock and engage autos, we would "tow in" the modules, or put them in an X-shape so that the swerve drive does not slide off the charging station. For example, in our preload taxi dock and engage auto:

```java
public static CommandBase preloadTaxiChargeBackwardsSLOW(SwerveDrivetrain swerveDrive, MotorClaw claw, Arm arm, Elevator elevator) {
    return sequence(
        deadline(
            waitSeconds(13.5), 
            sequence(
                ChargeAutos.preloadHigh(arm, elevator, claw),
                deadline(
                    taxiChargeBackwardsSLOW(swerveDrive),
                    run(() -> arm.moveArmMotionMagic(elevator.percentExtended())),
                    run(() -> elevator.moveMotionMagic(arm.getArmAngle()))
                )    
            )
        ),
        runOnce(() -> swerveDrive.towModules()), // Set the module states to towed in
        waitSeconds(0.2),
        runOnce(() -> swerveDrive.stopModules())
    ).finallyDo((x) -> swerveDrive.getImu().setOffset(180));
}
```

The problem with this is that the PID controller for turning the modules to their target position is only running once. This causes the wheels to all start spinning to start going towards the tow position, but not slow down.

To fix this issue, we separated setDesiredState into two different methods:

```java
public void run() {
    desiredState = SwerveModuleState.optimize(desiredState, Rotation2d.fromRadians(getTurningPosition()));

    desiredAngle = desiredState.angle.getDegrees();

    double velocity = desiredState.speedMetersPerSecond / ModuleConstants.kDriveTicksPer100MsToMetersPerSec 
                                                        / ModuleConstants.kDriveMotorGearRatio;
    this.desiredVelocity = velocity;
    
    if (this.velocityControl) {
        driveMotor.set(ControlMode.Velocity, velocity);
        this.currentPercent = 0;
    } else {
        this.currentPercent = desiredState.speedMetersPerSecond / SwerveDriveConstants.kPhysicalMaxSpeedMetersPerSecond;
        driveMotor.set(ControlMode.PercentOutput, this.currentPercent);
    }
    
    double turnPower = turningController.calculate(getTurningPosition(), desiredState.angle.getRadians());
    currentTurnPercent = turnPower;

    turnMotor.set(ControlMode.PercentOutput, turnPower);
}

public void setDesiredState(SwerveModuleState state) {
    if (Math.abs(state.speedMetersPerSecond) < 0.001) {
        state.speedMetersPerSecond = 0;
    }

    this.desiredState = state;
}
```

By separating setDesiredState() into run() and setDesiredState(), we avoid issues with the swerve modules not properly moving towards the desired state, as run() will always be run in the periodic method of SwerveDrivetrain.java, except when in test mode:

```java
/**
 * Have modules move towards states and update odometry
 */
@Override
public void periodic() {
    if (!DriverStation.isTest()) {
        runModules();
    }

    poseEstimator.update(gyro.getRotation2d(), getModulePositions());

    // Vision pose estimation
    if (sunflower.getPose3d() != null) {
        poseEstimator.addVisionMeasurement(sunflower.getPose3d().toPose2d(), Timer.getFPGATimestamp());
    }
}
```