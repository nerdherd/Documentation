# Overview
We use limelights for object detection for cubes and cones as well as odometry. 

# Limelight 
The limelight is how our robot gets vision. It allows pose estimation and movement based on the position of our robot. We use multiple pipelines to track different things, for example, our pipeline 2 allows us to track cubes while our pipeline 4 tracks april tags. It is important to tweak variables on the limelight dashboard to optimize tracking and recognition. When tracking the cube, turning up the exposure allows the limelight to detect its color. Yet, when tracking apriltags, we turn down the exposure to improve our motion-blur resilience.  

# Vision Odometry
Using our limelights, we could track our robot’s position based on the april tags around it. We implemented the position estimator so that we could add vision to our odometry, which estimates the position of the robot on the field. It is important that the limelight is higher or below the april tags, because being head-on causes “tag-flipping”. Also, when practicing with the april tags, it is important to make them as flat as possible. One of the problems were how our robot kept showing on the botton left corner. To implement field2d, we had to change the x and y field offsets for the vision coordinate system to work with the field2d coordinate system. The field2d coordinate system has bottom left as the origin, while the limelight helpers.java uses the middle of the field as the origin. We used limelight helpers, link below, for our limelight apriltag odometry.
https://github.com/SterlingHS/ChargedUP2023/blob/main/src/main/java/frc/robot/LimelightHelpers.java

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
Above is a picture of how we implement the vision readings to the swerve odometry. Sunflower is the class we use to create a Pose3d of our robot's location based on the LimelightHelpers.java file. 

# Drive to Object
Cube to move the robot is going to move to cube. So, use this to move is good. I think that we upgrade the robot.
Drive to object uses the limelights to detect the color of the cube. We haven't made our robot move to the target yet, but we have the x and y values for speed.
