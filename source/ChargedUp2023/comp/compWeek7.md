# Competition Week 7
*Week 14 (4/9 - 4/15)*

## Assembly

### 04/10 Monday 

- Battery testing 
- Packing/clean up for Houston 
- Continue assembling elevator
- Attach weight and battery plates to robot

![image](https://github.com/nerdherd/Documentation/assets/72529534/b33e6d88-6eed-48fe-a835-eca3f3fd0bc2)

- Work on spare claw
- Bumpers
- Take off fabric (both blue and red), Fabric layout
  - Update bumper documentation

### 4/14 Friday 

- Houston packing finalization
- Test batteries
- Scouting battery connections
- Elevator assembly

- Spare claw assembly

![image](https://github.com/nerdherd/Documentation/assets/72529534/407f3b9f-fb0d-4713-8075-fde20c13bd3d)

- Continued making bumpers
- Painted battery cart

![image](https://github.com/nerdherd/Documentation/assets/72529534/ae3390a6-5212-4df3-a783-dd811ed0b1e3)

### 4/15 Saturday

- Tested 775 motors
- Finished testing batteries
- Finished assembling elevator

![image](https://github.com/nerdherd/Documentation/assets/72529534/8e64897f-a7ad-41a3-ae03-17ec905d08bf)

- Finished replacing threads
- Finished spare claw assembly
- Finished bumpers

![image](https://github.com/nerdherd/Documentation/assets/72529534/53b3bb89-a0cd-40c5-a8fb-cbdfbc178d84)

- Finalized packing

## Programming

### Autos

This week, we finalized our taxi charge auto. This auto scores a preloaded cone onto the high node, then drives over the charge station and back on to engage.

We added a deadline of 13.5 seconds to the auto, which allows the swerve to tow its modules in and lock them, stopping it from falling off of the charge station.

Additionally, we found that decreasing the speed of our auto made it more precise. We were able to decrease the speed because of mechanical changes that smoothed out our belly pan, stopping it from colliding with the charge station.

```java
public static CommandBase preloadTaxiChargeBackwardsSLOW(SwerveDrivetrain swerveDrive, MotorClaw claw, Arm arm, Elevator elevator) {
      return sequence(
          deadline(
              waitSeconds(13.5), 
              sequence(
                  ChargeAutos.preloadHigh(arm, elevator, claw),
                  deadline(
                      taxiChargeBackwardsSLOW(swerveDrive),
                      run(() -> arm.moveArmMotionMagic(elevator.percentExtended())),
                      run(() -> elevator.moveMotionMagic(arm.getArmAngle()))
                  )    
              )
          ),
          runOnce(() -> swerveDrive.towModules()),
          waitSeconds(0.2),
          runOnce(() -> swerveDrive.stopModules())
      );
  }
```
