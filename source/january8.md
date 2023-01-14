# January 8th Meeting

## Admin

Admin met with Ms. Sadhwani to finalize the January and February snack donations and parent pick-up sign-up genius. Some members worked on a follow-up for spirit wear and finished a form for propellor hats and pajama pants. We finished the majority of the business plan today, leaving out things that we could not do at the current moment in time. This included outreach and team information (we sent out a form for members to complete and are waiting for completion). Media finalized edits for the first recap video and gathered footage for the second recap video. Admin discussed potential awards we will submit for this season and potential nominations, including Dean’s List and Woodie Flower’s.  Later on that night, we prepared the pizza dinner and ended the day with more progress on the stand-up banner. 

*****

## Assembly

### Field elements 

We finished measuring, cutting and assembling the cube shelf, middle cone ramp, and half charge station

![Field Elements](images/Day2/fieldElements.png)

*Field Element Progress*

We tested the half charge station with our swerve drive base and robot from Deep Space. After testing, we found that the drive base interfered with the ramp and the robot was not able to drive up the ramp. We were able to figure out that the angles were slightly off from the official drawings. The actual charge station is also made of polycarb so we decided to add 2 pieces of polycarb onto one of the ramps to make the structure closer to the original and see if the wood is the one that is causing the interference. 

### Electrical on Prototype Bot 

We made two boards that we mounted onto each side of the robot. Components on each board:  

* Board 1: RSL, Radio, RoboRIO, VRM, PDP, Pressure Switch, Analog Pressure Sensor, and Pressure Gauge 

* Board 2: Pressure Regulator, Pressure Gauge, 2 T-Splits, Manual Shutoff Valve, PCM, and 2 Solenoids 

**Progress:**

* Cut peg board to size using vertical bandsaw  

* Zip tied components onto the peg board 

* Made all electrical and pneumatic connections within each board  

* Zip tied each board onto the metal posts 

* Zip tied compressor onto battery plate 

*****

## CAD

### Linear Actuator Claw
The intake subgroup decided to create a 1 piston intake for simplicity and weight. Thid intake had a 100% success rate with the pneumatic test bench. 10 trails each for cone and cube.  

![Linear Actuator Claw](images/Day2/linearActuatorClawDay2.png)

*Linear Actuator Claw CAD and Assembly*

**Links with pneumatic test bench:**

### Rotational Claw CAD/Assembly

We decided to create a 4 point of contact on 4, 4" wheels, supports cones in many configurations, better grip, new cylinder placement will allow for less play (not tested with cylinders yet)  

![Rotational Claw](images/Day2/rotationalClawDay2.png)

Iteration 2: cone hits the base wheel and wood arms hit first before the compliant wheels so less grip, and turning mechanism has too much play. 
Iteration 3: 4 points of contacts on 4, 4" wheels, supports cones in many configurations, better grip, new cylinder placement will allow for less play. 

*Rotational Claw CAD and Assembly*

### Scissor Claw CAD/Assembly

This design is designed to have the functionality to pick the cone on its side and upright as well as to  intake the cube it would get fed by the wheels and end in a diamond shape.  

![Scissor Claw CAD](images/Day2/scissorClawCAD.png)

*Scissor Claw CAD*

![Scissor Claw Assembly](images/Day2/scissorClawAssembly.png)

*Scissor Claw Assembly*


### Elevator

We spent the day CADing the first design of the elevator. We first made a place for the elevator that doesn’t bump into anything using a crayola sketch. We then created an elevator taking inspiration from our 2019 robot, Gigantor. This was our final product.  

![Elevator Crayola CAD](images/Day2/elevatorCrayolaDay2.png)

*Elevator Crayola CAD*

![Elevator CAD](images/Day2/elevatorCADDay2.png)

*Elevator CAD*

However, while consulting with our main mentor, he mentioned that the weight lighting bars will not be accurate and will take too long to manufacture. He also mentioned that the gusset that holds the bearing will only have 1 full side of bearings and 2 sides only half with bearings, making it more inaccurate. He also mentioned that we did not need to make the carriage long. Taking that into consideration, we decided to start a new iteration that will be closer to what we will first manufacture. 

![Sliding Gusset CAD](images/Day2/slidingGussetCADDay2.png)

*Sliding Gusset CAD*

This was the sliding gusset that we had prototyped. This captured both sides, and the bar will be touched 12 bearings.  

*****

## Manufacturing

### Swerve

During pre-season, we CAMed the elevate and up bars (handles) for the swerve drive. This was made for easier transport of the swerve drive. We split into 2 groups (each group working on separate TM-1 CNC mills) and completed the manufacturing of the elevate and up bars. The gussets for these bars were completed prior to kickoff. 

![Handles for Swerve Drive](images/Day1/mfghandlesDay2.png)

*Handles for Swerve Drive*

### Claw

We also 3d printed and laser cut parts for the claw prototypes. 

![3D Claw Print](images/Day2/mfgprintDay2.png)

*3D-Printing for Claw Prototypes (Linear Actuator Claw)*

![Lasered Claw](images/Day2/mfglaserDay2a.png)

![Lasered Claw](images/Day2/mfglaserDay2b.png)

*Laser cutting for claw prototype (Rotational Grip Claw)*

*****

## Programming

### Vision, Arm, Claw

Today, our group had two main goals: complete the base repository (with arm and claw subsystems), and recognize April tags using Photon vision. 

Our first goal of completing the base repository was quick, as most of the code was written yesterday. Today we added a method of controlling the arm using percent output and a joystick as a simpler intermediate between newly constructed hardware and motion magic control using PID. The latest version for today can be found [here](https://github.com/nerdherd/ChargedUp2023/tree/387af596c2bf5fcec82245eb6617aae20f59fdf3). 

After the team-wide code review, we marked refactoring changes to be implemented tomorrow. 

Our second goal of recognizing April tags using Photon vision was slightly more difficult. We were unable to open the PhotonVision dashboard and thus not letting us set a static IP address for the limelight, so we continued to use a dynamic IP address which allowed us to identify April tags and read data such as pitch and yaw. 

![Testbench Setup](images/Day2/testbenchSetup.png)

*Image of testbench setup*

![Network Switch Setup](images/Day2/networkSwitchSetup.png)

*Image of network switch setup*

### Autonomous Pathing

Today, our group’s goals were to finish creating two simple auto paths (moving backwards and forwards) using tank drive. After the autos were finished programming, we did a systems check on Gigantor (our 2019 robot) so that we could ensure there were no hardware issues with the robot before testing the autos. From the systems check, we found that Gigantor’s chain was skipping. Due to this hardware issue, we were unable to test the autos.  

### Swerve

Today our group’s goals were to update our swerve drive code to WPILib 2023 and be able to run it on the robot. The upgrading process itself was relatively straightforward, with the only major code change being having to convert Swerve Module states into Swerve Module Positions, as in 2023 WPILib, SwerveDriveOdometry updates using Swerve Module Positions, which contain the distance travelled and the angle of one swerve module, rather than Swerve Module States, which contain the speed and angle instead. We ran into several issues, such as there not being an official NavX library for WPILib 2023, and a strange issue where all angles were rotated by 90 degrees. We applied temporary fixes to most of these issues, as we were short on time, using an unofficial NavX library in place of the official one (which can be found here: https://github.com/rzblue/navx-frc) and manually applying a rotation to all angles. We also tested driving onto the mock charging station that our assembly team built but we were not able to drive onto it, as the frame would hit the ramp of the charging station before the wheels were able to contact it. 
