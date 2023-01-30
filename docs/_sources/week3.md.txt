# Week 3 (1/21 to 1/28)

```{admonition} Under Construction
This page is currently under construction. Please return later for more updates.
```

## Assembly



## CAD



## Manufacturing



## Programming

### Vision Group

#### 1/23

We got the April Tag and Object Detection to work on a single limelight. The 4 objects being the cones, cubes, tape, and April Tags. Our code allows us to have the robot drive toward a target object while also making any angle corrections along the way. 

![Tank drive in front of target](images\Week3\prgVision1.png)

Later in the day, we refactored the aimAt_Object_() methods into one aimAt() method which allows the code to choose to target any of the 4 object types in one line only by entering in an enum: “CONE”, “CUBE”, “TAPE”, “TAG”. 

```java
public static enum TargetType {
   CONE,
   CUBE,
   TAPE,
   TAG 
}
```

The object detection works so well that we can tape an object to a moving person and have the robot chase them around completely autonomously. As an extra feature, we implemented a move back algorithm which has the robot drive backwards if the object were to get too close. 

#### 1/27

We worked on implementing vision with the swerve drive. We did this by creating a command that combined the turnToAngle command and the driveToTarget command. We were able to test our code on the actual swerve drive, but it didn’t work. One of the possible errors was that the PID values needed to be tuned a little bit. 

![Swerve in front of target](images/Week3/prgVision2.png)

*DriveToTarget testing, robot oscillated in place*

#### 1/28

We refactored our code for vision with the swerve drive. We switched the xSpeed and ySpeed values because the y and x axes are switched. 

Tested the previously broken limelight and it works now. Also reflashed the limelight with photonvision firmware to have limelight firmware. 

Tested our refactored code. The code seems to work but the values were flickering because the limelight was wavering between not detecting the apriltag and detecting the apriltag. So, we need to tune the limelight more. 

![Limelight](images/Week3/prgVision3.png)

*Previously broken but now functional limelight*


