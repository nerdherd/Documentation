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

As seen in those code segment we added logging to the cube shooter code. We added a new tab on Shuffleboard called "Wrist" then proceeded to add certain cases to appear on Shuffleboard depending on the switch level. 

### Creating the Shooter

```java

```
