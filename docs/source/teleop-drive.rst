Drive
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

.. code-block:: console

   (.venv) $ pip install lumache
   
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

