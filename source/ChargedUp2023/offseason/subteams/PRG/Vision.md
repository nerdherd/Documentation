# Overview
Earlier in the season we were using limelights for object detection, cubes and cones. 

# Limelight 
The limelight is how our robot gets vision. It allows pose estimation and movement based on the position of our robot. We use multiple pipelines to track different things, for example, our pipeline 2 allows us to track cubes while our pipeline 1 tracks april tags. It is important to tweak variables within these pipelines to optimize the best tracking. When tracking the cube, turning up the exposure allows the limelight to detect the color of the robot. Yet, when tracking apriltags, we turn down the exposure to improve our motion-blur resilience. We used limelight helpers, shown at the bottom, for most of our limelight code.
https://github.com/SterlingHS/ChargedUP2023/blob/main/src/main/java/frc/robot/LimelightHelpers.java 

# Vision Odometry
Using our limelights, we could track our robot’s position based on the april tags around it. We implemented the position estimator so that we could add vision to our odometry, which estimates the position of the robot on the field. It is important that the limelight is higher or below the april tags, because being head-on causes “tag-flipping”. Also, when practicing with the april tags, it is important to make them as flat as possible. One of the problems were how our robot kept showing on the botton left corner. We had to change the x and y field offsets for the vision coordinate system to work with the field 2d coordinate system. The field 2d coordinate system has bottom left as the origin, while the limelight helpers.java uses the middle of the field as the origin.

``` java
     /**
     * Have modules move towards states and update odometry
     */
    @Override
    public void periodic() {
        if (!DriverStation.isTest()) {
            runModules();
        }
        // odometer.update(gyro.getRotation2d(), getModulePositions());
        poseEstimator.update(gyro.getRotation2d(), getModulePositions());
        Pose3d sunflowerPose3d = sunflower.getPose3d();
        if (sunflowerPose3d != null) {
            poseEstimator.addVisionMeasurement(sunflowerPose3d.toPose2d(), Timer.getFPGATimestamp());
        }
        field.setRobotPose(poseEstimator.getEstimatedPosition());
    }
```
Above is a picture of how we implement the vision readings to the swerve odometry. Sunflower is the class we use to create a Pose3d of our robot's location. 

# Drive to Object
Cube to move the robot is going to move to cube. So, use this to move is good. I think that we upgrade the robot.
Drive to object uses the limelights to detect the color of the cube. We haven't made our robot move to the target yet, but we have the x and y values
