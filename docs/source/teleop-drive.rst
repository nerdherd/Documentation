Teleop Drive
=====

.. _installation:

Installation
------------

To use be able to write Java code for our robots, first install the latest version of  `WPILib VSCode <https://github.com/wpilibsuite/allwpilib/releases/tag/v2022.4.1>`_

.. _creating-a-new-project:

Creating a New Project
------------

.. _motor-and-controller-configuration:
Motor and Controller Configuration
------------

The first thing you want to do is find out what motor controllers the robot is using. The common ones used on our team is TalonFXs (Falcon motors) and TalonSRXs. You can find which motor controllers the robot is using from Phoenix Tuner to be able to configure your motors as shown here:

.. code-block:: console

   public class Drivetrain extends SubsystemBase {
       public TalonFX rightMaster;
       public TalonFX leftMaster;
       ublic TalonSRX rightSlave;
       public TalonSRX leftSlave;
   }

You also need to configure your controller(s) in RobotContainer.java. The snippet below shows how to configure XBox and PS4 controllers:

.. code-block:: console

   public static XBoxController driveController = XboxController(0);
   public static PS4Controller operatorController = PS4Controller(0);
   
.. _teleop-drivebase-code:
Teleop Drivebase Code (Tank Drive)
------------

To get working drivebase code for teleop:

1) Setup the drivebase in robotInit()

   - Find the motor ports from Phoenix Tuner
   - Bind the previously created motors to instances of your motor type with the port number
   - Make the slave motors follow their respective master motors with the *follow* method
   - Set one side of the robot to inverted (because of how the drivebase is built, one side needs to be inverted)

.. code-block:: console

   rightMaster = new TalonFX(0);
   leftMaster = new TalonFX(1);
   rightSlave = new TalonSRX(2);  
   leftSlave = new TalonSRX(3);

   leftSlave.follow(leftMaster);
   rightSlave.follow(rightMaster);

   // Inverted the right side
   rightMaster.setInverted(true);
   leftSlave.setInverted(InvertType.FollowMaster);
   rightSlave.setInverted(InvertType.FollowMaster);
   
2) Retrieve joystick inputs in teleopPeriodic()

   - Create a variable for each joystick
   - Assign the controller's axis input to the variable

.. code-block:: console

   double leftInput = OI.ps4Controller.getLeftY();
   double rightInput = OI.ps4Controller.getRightY();

3) Set power for the joystick inputs after retrieving joystick inputs in teleopPeriodic()

   - Make the master motors move linear to the joystick inputs
   
.. code-block:: console

   leftMaster.set(ControlMode.PercentOutput, leftInput);
   rightMaster.set(ControlMode.PercentOutput, rightInput);
