# Week 10 (3/12 - 3/18)

```{admonition} Under Construction
This page is currently under construction. Please return later for more updates.
```

## Assembly

## CAD

## Manufacturing

## Programming

### Vision Group

We changed our code structure for vision autos so that they were split up into smaller parts. We also changed the deadband for vision which uses speed.

```java
if (NerdyMath.inRange(xSpeed, -.1, .1) &&
    NerdyMath.inRange(ySpeed, -.1, .1) &&
    NerdyMath.inRange(rotationSpeed, -.1, .1))
    {
        chassisSpeeds = new ChassisSpeeds(0, 0, 0);
        SwerveModuleState[] moduleStates = SwerveDriveConstants.kDriveKinematics.toSwerveModuleStates(chassisSpeeds);
        drivetrain.setModuleStates(moduleStates);
        currentCameraMode = CAMERA_MODE.ARRIVED; 
    }
    else{
        chassisSpeeds = new ChassisSpeeds(xSpeed, ySpeed, rotationSpeed);
        SwerveModuleState[] moduleStates = SwerveDriveConstants.kDriveKinematics.toSwerveModuleStates(chassisSpeeds);
        drivetrain.setModuleStates(moduleStates);
        currentCameraMode = CAMERA_MODE.ACTION;
    }
```