### Overview

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
```
We created the shooter for the cube spammer in code, which works by creating a left and right TalonFX motor. The motors are both put into neutral mode upon initializing 
