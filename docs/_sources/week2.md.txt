# January 13

## Assembly

### Training

We conducted training for new members (Rotations):  
Motor testing 
- Used phoenix tuner and driver's station 
- Recorded motor data in a spreadsheet and labeled motors 

Comp maintenance 
- Pit checklist  

Taught Pneumatics 
- How to use the manual test bench 
- Layout and components of prototype bot pneumatics

### Claw

Once the assembly of the double piston claw was done, we attached it to the prototype bot.  

![Claw](images/jan13/asmclaw.png)

*Image of the completed claw assembly*

### Field Elements

We finished assembling the end cone ramp. 
Connected the cube shelf divider beam to cone ramp horizontal beam using wood screws and spacer plywood 

![Cone Ramp](images/jan13/asmConeRamp.png)

*Image of the completed Cone Ramp.*

### Other

We repaired the Wooden Dolley our team uses to push around large materials. 
- Replace broken plywood 
- Stapled fabric using staple gun 

![Wooden Dolley](images/jan13/asmDolley.png)

*Fixed Wooden Dolley*

We also assembled versaplanetary gearboxes for our prototype bot. 

We started working on our new robot cart and driver’s station. 
- brainstorming updated designs 
- design constraints 
- additional features

## CAD

### Telescope Arm

First cad of two stage telescope arm. Each tube is 27 inches long. Received feedback. Need to find a way to move the arm. Thinking of attaching motor to elevator carriage. 

![Arm](images/jan13/cadArm.png)

*Screenshot of arm CAD*

### Elevator

We finished updating the elevator. Some of the updates included making the bars into 29 inches to make it easier for manufacturing. We created drawings of all the parts, and created a BOM that we must order to make the elevator.  

![Elevator](images/jan13/cadElev.png)

*Screenshot of elevator CAD*

### Swerve Bumpers

After testing dimensions with a current swerve drive base docking and engaging we completed the swerve bumper design with technical drawings from those dimensions. We wanted to make the process of taking off bumpers and putting them back on as easy as possible. We went with a pin design with 4 c-channel mounts with two on opposite sides. 

![Drawings](images/jan13/cadBumper1.png)

![Drawings](images/jan13/cadBumper2.png)

*Screenshots of the drawings for our swerve bumpers*

### Rotational Claw

We then tested the rotational claw with the pneumatic piston test bench and had 100% success rate out of 10 trials with cone and cube.

![Claw](images/jan13/cadClaw.png)

*Screenshot of the claw cad.*

## Manufacturing

The manufacturing subteam set up a 3D printer with TPU filament and another with Nylon X to test the usability of the various materials. We printed a test belt with the TPU, which proved to be successful. We also reorganized and lowered our stock rack so that we could add more shelves and create a more efficient storage area for manufacturing. Furthermore, the side guards on the TM-1 were removed in preparation for the elevator bar. The TM-1 vises and work surface, as well as the side guards, were vacuumed and cleaned with oil. 

![TM-1](images/jan13/mfg1.png)

*A close-up of the tidied bare TM-1 work surface. *

![TM-1](images/jan13/mfg2.png)

*A full shot of the TM-1 with its guard railing removed.*

![MFG](images/jan13/mfg3.png)

*A selfie shot of the people who busted their butts and worked through approx. 10 machine cloths to get this baby nice and shiny.*

![TM-1 part](images/jan13/mfg4.png)

*A full shot of our cleaned guard railing with its screws and washers (for connection to the TM-1) taped on to ease reattachment + the tips of my feet (how scandalous). *

## Programming

#### Vision Group

This week, we learned that there are two methods of determining the robot’s distance from the april tags using the Limelight. The first method uses the angle and the height of the camera along with the angle and height of the april tag to determine the distance from the camera to the target. It also uses the angle from the Limelight to the target which is the value that is changed to help determine the distance between the Limelight and april tag. However, if the numbers were slightly off, then the distance would be changed exponentially. That is why we decided to go with the second method that uses the area of the Limelight which the target takes up. To do so, we had to find an equation to determine how the area of the target relates to the distance between the Limelight and the april tag. We tested the turning using the pitch received from the Limelight, and it was successful 

#### Auto Group

First, we continued testing the drive and claw functionalities of the prototype bot. For the sides of the drive base that had an unused motor, the motor current ramped up to around 178 amps.  The removal of the motor resulted in the motor current ramping up to only around 30-40 amps, which is a safe amount.  Next, we tested autos that drove straight and faced a certain angle using a NavX, but they need further PID tuning. We have also tested several buddy climb iterations.  There were some successful trials; however, the swerve drivetrain was unable to stay on the buddy climb for most trials. 

#### Swerve Group

