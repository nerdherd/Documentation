# Competition Week 3
(Week 10 (3/12 - 3/18))

```{admonition} Under Construction
This page is currently under construction. Please return later for more updates.
```

## Assembly

## CAD

### 3/13 

In order to improve our strategy and help scout teams for alliances, we held a strategy meeting and created a strategy cheat sheet to help our members efficiently scout during our regionals.  

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