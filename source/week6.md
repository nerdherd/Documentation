# Week 6 (2/12-2/18)

```{admonition} Under Construction
This page is currently under construction. Please return later for more updates.
```

## Assembly

## CAD

## Manufacturing

## Programming

-We added code for the elevator to the Constants, RobotContainer, Arm, and elevator folder. We updated the CANSwerveModule by switching to directly reading from CANCdoer for angles. We also tuned the encoder offsets for our CAN Swerve Modules.

For our superstructure, we separated our arm and elevator into separate classes to make programming them easier. We also updated our feed forward values and calculations. We also added code for limit switches, allowing us to reliably set our stow position. This stops our pivoter from overshooting. We also added buttons for resetting the encoders of both subsystems in the superstructure to make testing simpler.

For our swerve drive, we created simulations to test our dodge mode and allow our drivers to experiment with our drive filters. 

![Swerve Simulations](./images/Week6/swerveSimulations.png)

*Swerve simulations for driver input tuning*

We also abstracted our filters into separate Filter classes sharing an interface, making it easier to apply different filters. This allowed us to create a more complex filter pipeline without adding a lot of extra code to our SwerveJoystickCommand class. We then separated out this code into a new repository, [NerdyFilters](https://github.com/nerdherd/NerdyFilters). 

```java
Filter driveFilter = new FilterSeries(
    new DeadbandFilter(deadband),
    new WrapperFilter(
        (x) -> {
            if (x == 0) {
                belowDeadband = true;
                return 0.0;
            } 
            if (x > 0) {
                belowDeadband = false;
                return x - deadband;
            } else {
                belowDeadband = false;
                return x + deadband;
            }
        }
    ),
    new ExponentialSmoothingFilter(alpha),
    new PowerFilter(3),
    new WrapperFilter(
        (x) -> {
            if (belowDeadband) return 0.0;
            else {
                return Math.signum(x) * ((Math.abs(x) / deadbandScaler) + motorDeadband);
            }
        }
    ),
    new WrapperFilter(
        (x) -> {
            return Math.signum(x) 
                * slewRateLimiter.calculate(Math.abs(x));
        }
    ),
    new ScaleFilter(scale),
    new ClampFilter(scale)
)
```

*Our filter pipeline*

For vision, we measured optimal mounting heights and angles for our limelights. Additionally we tried out using PhotonVision, as it makes cone detection less noisy, when in combination with a rolling average filter.

![Vision Tuning using Glass](./images/Week6/visionGlass.png)

*Reading vision values in Glass*
