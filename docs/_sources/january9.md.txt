# January 9th Meeting

## Asssembly

---

## CAD


---

## Manufacturing

### Swerve

With the completed Up and Elevate bar and the gussets, we assembled the handles on the swerve drive. 

![Swerve Handles ASM](images/Day3/mfghandlesDay3.png)

*Completed assembly of the handles for swerve drive.*

### Elevator & Claw

We also 3D printed parts for the claw/intake prototypes (Elevator and Scissor Claw; respectively) 

![3D Elevator Print](images/Day3/mfgprintDay3a.png)

*Printed elevator parts.*

![3D Claw Print](images/Day3/mfgprintDay3b.png)

*Printed Scissor Claw part.*

![Linear Actuator](images/Day3/mfgclawDay3.png)

*Laser cut linear actuator prototype and assisted with the assembly*

### Other

We also 3D printed a cover for the Navx on the roborio.

![3D Navx Cover Print](images/Day3/mfgprintDay3c.png)

*Finished print of the Navx cover.*

All the machines (TM-1 and the Super Mini Mills) and the vises were cleaned for Friday.  

![Cleaning](images/Day3/mfgDay3.png)

*Cleaning the machines*

---

## Programming

### Brianna's Group
#### Vision

Today, our goal was to drive within range of and align to an April tag using a tank drivebase. We began with a code review with a mentor and then merged our testbench code with the main repository: ChargedUp2023. We then referred to PhotonVision documentation to implement an aim at target method. This method used a PID loop with the error being the yaw difference between the target and limelight.  

![Vision Code Sample](images/Day3/progvisonDay3.png)

*Vision Code Sample*

Our implementation of distance finding between target and camera was similar: where distance was used as the error for a PID loop. After implementing this functionality using documentation, however, we found there was a high error (anywhere from 10 to 90 meters of error) when printing the distance. After manually calculating distances and ensuring the built-in equation (see below) was correct for our use case, we realized the high error was because of our low accuracy when measuring the height of the camera and the height of the limelight. 

![Vision Code Sample](images/Day3/progcameraDay3.png)

*Built-in Equation*

#### Radio Configuration

Additionally, we found that two radios we owned would not establish communications on driver station. This issue could also be seen on the indicator lights on our network switch, where the light corresponding to the radio would not turn on (see image below). This was likely because they were not configured, and a future goal is to ensure at least one of our laptops is reliable when configuring radios. 

![Network Switch](images/Day3/progradioDay3.png)

*Network switch with all indicator lights off.*


### Kyle's Group
#### Swerve Code

Today, our goal was to finish testing swerve drive code on 2023 and begin programming commands such as turning to an angle and automatically balancing on the charging station. We found that most of our issues from yesterday were due to the encoders becoming offset. We were able to fix this by resetting the encoders to the same position as the absolute encoders, using this method: 

![Encoder Fix](images/Day3/progencoderfixDay3.png)

*Code sample that reset the encoders to the same position as the absolute encoders.*

After fixing the program, we were able to have our driver test driving the swerve drive. We then added a low pass filter and scaled the input quadratically to make the driving more comfortable for them, using these lines of code: 

![Drive Code](images/Day3/progdrivecodeDay3.png)

*Code sample for the low pass filter and scaled the input quadratically*

We used both the low pass filter and the quadratic filter last year, so we used nearly the same implementation as our Rapid React code in this project. 

While our driver tested the swerve drive, our assembly subteam set up their new mock charging station, which now has a layer of plexiglass on top to more accurately match the real charging station. This allowed our swerve drive to climb the charging station. After a bit of practice, our driver was able to regularly climb the charging station and park on top of it.  

Afterwards, the swerve drive was given to the assembly subteam to add handles and bumpers to it. While assembly worked on the drivebase, we continued in development, writing a new command for turning to an angle based on the NavX’s readings, adding javadoc comments and more documentation to our code, and refactoring some of the classes to be more readable. After Assembly finished, we were able to drive onto the ramp even with a bumper on the robot, showing us that swerve drive may be a feasible choice for this season. However, we still need to fix much of our code, as it lacks important functionality such as in-game autonomous routines, and some functions, such as turn to angle, either weren’t tested or don’t work. We plan to fix these soon and implement them in a swerve drive auto. 


### Ayaka's Group
#### Autonomous Code

Today, our goal was to finish writing up the auto commands and writing a drivetrain code that extends from the differential drive train class on WPILib.  By testing on the prototype bot and Thomas (our 2020, 2021 robot), we found out that the code we wrote for the drivetrain did not work so we shifted to the code from yesterday and tested.  We discovered that there were some issues with one of the Falcon motors in the drive and wrong inversions on the right side of the drive base; however, we were able to troubleshoot by using Phoenix Tuner to check what they were inverted to and editing code as needed.  

#### Claw Code

We also tested the claw code and found out that we were using faulty solenoids, so we switched them out and successfully controlled the claw. 
