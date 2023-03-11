# Week 5 (2/6 to 2/11)

## Assembly

N/A

## CAD
2/5/23: 

-Elevator drawing: We finished the battery plate for the comp bot and started 3d printing spacers for our elevator. We also talked to the assembly subteam about how the robot will go together. Drawings for the elevator were also created and edited. Finally, we did testing for different claw prototypes and changed the swerve bumper design.

Week 5: CAD Elevator Drawing Image


2/6/23:

-Heeseung: Assembled Elevator

-Kloe: Worked on modified L brackets for bumper, swerve module covers began printing  

-Joyce: We finished assembling the elevator! We attached the motor and chained the second stage string. The bot should be competition ready shortly. 

Week 5 Elevator Finished Assembly Image


2/11/23
 

-Kloe: Finished priniting swerve module covers  

-Joyce: We did some assembly work for our bumpers and helped to mount the electrical panels onto the robot. We also worked on creating covers for the swerve modules. Finally, we made hardstops for the elevator. 

## Manufacturing


2/6  

On Monday’s meeting, the manufacturing subteam completed manufacturing the 1.5x1 gussets, cross beam, and studs for the pivot frame. Furthermore, the swerve drive cross bar was manufactured and sent to assembly. 



2/7 

On Tuesday, we manufactured the BUD, 1.5x3, and 2x3.5 gussets and the DIAG bar for the pivoter frame.  
The manufacturing of the DIAG bar in progress. 


2/8 

The BOTGUSS and TOPGUSS were completed in the mini mill, but not post-processed. 


2/9  

The BOTGUSS AND TOPGUSS were bandsawed, sanded, and buffered, and a new sheet was loaded in for the battery plate. The battery plate program was run and post processed. 
The battery plate installed at the bottom of our bot. 
A swag back shot of one of our members machining gussets. 


2/10 

There were 3 leftover TOP gussets that were unable to fit onto the first machined sheet. Heart gusset keychains for our mini mill team members and mentor were also added onto the sheet due to an abundance of space. Both were manufactured, and the CAM for the NERDHERD backplate as well as the motor mount were completed. 
Our completed heart gusset keychains. 
A selfie after 45 minutes of bandsawing, sanding, and buffering the curved edges. 
Our CAM of the NERDHERD backplate. 


2/11 

On Saturday, we manufactured the NERDHERD backplate and motor mount, which were then attached to the bot. The wrist bar was also completed. 

A picture with the completed NERDHERD backplate. 

The motor mount attached to the vertical bars. 


## Programming


2/7/23

-We drew some diagrams to plan where the two limelights should be on the robot. Both limelights will be on the left and right side of the robot and one will be placed higher than the other to see objects that the lower limelight cannot. We also mapped out what each button on the driver and operator controller will do. We decided that holding the button to drive to one of the objects (Apriltag, reflective tape, cone, cube) would be controlled by the driver, while non-driving functions (claw extend, claw close, arm extend, arm retract) and switching between the two limelights would be controlled by the operator.  

-Week 5: Button Diagram Picture

-Week 5: Limelight Picture

-After planning out how we want to map each button, we started revamping the vision class so it would manage both limelights.  

-Inside the vision class there are methods to switch between the two limelights and to change the pipeline to detect different objects. We also reworked the DriveToTarget and ApproachCombined commands to be compatible with the improved vision class. Once we were done with that, we created button bindings for what we had planned out earlier. We could not test our code on the robot, so we started making a vision testbench to calibrate the limelights. 


2/13/23

-Swerve Group 

Week 5: Swerve Program

This week we worked on a dodge mechanism that changes the pivot point of the robot to rotate around another robot. We developed code for the cone runner that works! We also have motion magic code, but we have not tested it. Swerve modules have been updated to be compatible with CANCoders besides the normal mag encoders.  


-Tank/Subsystems Group 

This week we worked on testing a new prototype of a claw with a motor, a new iteration of the linear claw, and a prototype of the cone runner. Additionally, we tuned Motion Magic for the arm. We also wrote code for the elevator and worked on our software binder. 


