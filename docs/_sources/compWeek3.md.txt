# Competition Week 3
*Week 10 (3/12 - 3/18)*

## Assembly

### 3/13 Monday

Pack for LAR  
* Explained packing lists & BOMs 

Batteries  
* Members finished battery leads 
* Testing in progress 

Sensors electrical 

Allen Wrenches Sizes Review 

Vp gearbox review  

Fixed bumpers  

Laser cutting procedure 

### 3/20 Monday

Cleaning 
* Cleaned electrical benches 

Packing 
* Check the packing 
* Made a list of missing items 

Reflections on Competition 
* Reflect on pluses and deltas from the Los Angeles Regional competition 

Bumpers 
* Fixed the red bumpers 

### 3/24 Friday

Packing 

LAR Reflection 

Cleaning 

Chain tensioning system for spool idle sprocket, freespin, ziptie to tension 

Fix bumpers 
* Replace pool noodles 
* Double check for other issues 

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