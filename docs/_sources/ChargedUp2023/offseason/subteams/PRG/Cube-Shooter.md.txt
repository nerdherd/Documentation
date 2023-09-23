## Overview

The cube-shooter is the robot we plan on using at the upcoming off-season competition Chezy-Champs. The purpose of it is to pick up cubes as the robot drives into them, allowing for quick intake, and then shooting the cube back out into either the low, mid, or high shelves. 

## Code Review

### Adding Logging to the Wrist

```java
    public void initShuffleboard(LOG_LEVEL level) { 
        if (level == LOG_LEVEL.OFF || level == LOG_LEVEL.MINIMAL) {
            return;
        }
        ShuffleboardTab tab = Shuffleboard.getTab("Wrist");
        switch (level) {
            case OFF:
                break;
            case ALL:
                tab.addNumber("Motor Output", wrist::getMotorOutputPercent);
                tab.addString("Control Mode", wrist.getControlMode()::toString);
                tab.addNumber("Wrist Target Velocity", wrist::getActiveTrajectoryVelocity); 
                tab.addNumber("Closed loop error", wrist::getClosedLoopError);

            case MEDIUM:
                tab.addNumber("Wrist Current", wrist::getStatorCurrent);
                tab.addNumber("Wrist Velocity", wrist::getSelectedSensorVelocity);
                tab.addNumber("Wrist Voltage", wrist::getMotorOutputVoltage);
                tab.addNumber("Wrist Percent Output", wrist::getMotorOutputPercent);

            case MINIMAL:
                tab.addNumber("Current Wrist Ticks", wrist::getSelectedSensorPosition);
                tab.addNumber("Target Wrist Ticks", () -> targetTicks);
                tab.addBoolean("At target position", atTargetPosition);
                break;
        }
        }
```

As seen in this code segment we added logging to the cube shooter code. We created a new tab in Shuffleboard called "Wrist" then used the loggingLevel contsant we created to seperate the logs into different sections for the wrist. Depending on if the loggingLevel is OFF, ALL, MEDIUM, or MINIMAL, Shuffleboard will only show the tabs listed under each case, this way we reduce the amount of logs we used depending on what is needed. 

### Creating Shooter

```java
public Shooter() {
        TalonFX leftMotor = new TalonFX(ShooterConstants.kLeftMotorID);
        TalonFX rightMotor = new TalonFX(ShooterConstants.kRightMotorID);
        leftMotor.setInverted(false);
        rightMotor.setInverted(true);
        leftMotor.setNeutralMode(NeutralMode.Brake);
        rightMotor.setNeutralMode(NeutralMode.Brake);
        leftMotor.configVoltageCompSaturation(11);
        rightMotor.configVoltageCompSaturation(11);
        leftMotor.enableVoltageCompensation(true);
        rightMotor.enableVoltageCompensation(true);
    }
public CommandBase outtake() {
        return sequence(
            setPower(ShooterConstants.kOuttakePower),
            waitSeconds(0.25),
            setPowerZero()
        );
    }

    public CommandBase intake() {
        return sequence(
            setPower(ShooterConstants.kIntakePower),
            waitSeconds(0.25),
            setPower(ShooterConstants.kIntakeNeutralPower)
        );
    }

```

We created the shooter for the cube spammer in code, and then created an outtake command that waits 0.25 seconds to shoot before setting the power back to 0 so the cube-spammer is no longer outtaking. We also created an intake command which also waits 0.25 seconds before intaking the cube and then setting the power to neutral power, that way it is no longer intaking or outtaking.

### Added Button Bindings

```java
 commandDriverController.share().onTrue(Commands.runOnce(imu::zeroHeading));
    commandDriverController.options().onTrue(Commands.runOnce(swerveDrive::resetEncoders));
    commandDriverController.triangle().whileTrue(new TheGreatBalancingAct(swerveDrive));
    commandDriverController.circle()
      .whileTrue(Commands.run(() -> swerveDrive.setVelocityControl(true)))
      .whileFalse(Commands.run(() -> swerveDrive.setVelocityControl(false)));
    commandOperatorController.R1().onTrue(new InstantCommand(() -> wrist.moveWristMotionMagicButton((WristConstants.kWristGround))));
    commandOperatorController.R2().onTrue(new InstantCommand(() -> wrist.moveWristMotionMagicButton((WristConstants.kWristLow))));
    commandOperatorController.L1().onTrue(new InstantCommand(() -> wrist.moveWristMotionMagicButton((WristConstants.kWristMid))));
    commandOperatorController.L2().onTrue(new InstantCommand(() -> wrist.moveWristMotionMagicButton((WristConstants.kWristHigh))));
    upButton.whileTrue(new InstantCommand(() -> wrist.moveWristMotionMagicButton((WristConstants.kWristStow))));
```

We added button bindings to our cube-spammer code. We binded multiple commands to the buttons on the controller, including a low, mid, and high option for scoring, a ground button for intaking, a button for stowing the robot arm, a resetEncoder button, and a button for TheGreatBalancingAct, a command that balances the swerve drive on the charging station. 

########################################################################################################################################################################################################################################################################################################################################################################################################################################################################## Add Wrist Position Constants
