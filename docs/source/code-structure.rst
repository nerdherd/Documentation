Code Structure
=====

Motor and Controller Configuration
------------

The first thing you want to do is find out what motors controllers the robot is using. The common ones used on our team is TalonFXs(Falcon motors) and TalonSRXs. Next, find the ports using PhoenixTuner. Once you have found what CAN ports the motor controllers are, you can configure the motors as shown here:

.. code-block:: console

   private static TalonFX leftMaster = new TalonFX(1);
   private static TalonSRX rightMaster = new TalonSRX(2);
   
To retrieve a list of random ingredients,
you can use the ``lumache.get_random_ingredients()`` function:

.. autofunction:: lumache.get_random_ingredients

The ``kind`` parameter should be either ``"meat"``, ``"fish"``,
or ``"veggies"``. Otherwise, :py:func:`lumache.get_random_ingredients`
will raise an exception.

.. autoexception:: lumache.InvalidKindError

For example:

>>> import lumache
>>> lumache.get_random_ingredients()
['shells', 'gorgonzola', 'parsley']

.. _teleop-drivebase-code:
Teleop Drivebase Code
------------

.. _autonomous-drivebase-code:
Autonomous Drivebase Code
------------

