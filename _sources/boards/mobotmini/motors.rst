Motors
======

Mobot MINI has **two drive motors**:

- ``mobotMINI.left_motor`` for the left wheel
- ``mobotMINI.right_motor`` for the right wheel

To move the robot, choose direction and speed for each motor.

Direction
---------

Use the first value in ``set_direction_and_speed(direction, speed)``:

- ``0``: first rotation direction
- ``1``: opposite rotation direction

If your forward test moves backward, swap the direction value you use.

Speed (percent)
---------------

Speed is the second value and is a percentage:

- ``0`` = stop
- ``100`` = max speed
- ``30`` = slow and safe for indoor testing

A comfortable beginner range is usually ``40`` to ``70``.

Quick test
----------

.. code-block:: python

   print("Move forward at 60%")
   mobotMINI.left_motor.set_direction_and_speed(0, 60)
   mobotMINI.right_motor.set_direction_and_speed(0, 60)

   print("If this moves backward, change 0 -> 1 on both motors")

Turn example (with debug prints)
--------------------------------

.. code-block:: python

   print("Turn right in place")

   # Opposite directions + similar speed = pivot turn
   mobotMINI.left_motor.set_direction_and_speed(0, 55)
   mobotMINI.right_motor.set_direction_and_speed(1, 55)

   print("Turn command sent")

Stop and brake
--------------

.. code-block:: python

   print("Soft stop")
   mobotMINI.left_motor.stop()
   mobotMINI.right_motor.stop()

   print("Active brake")
   mobotMINI.left_motor.brake()
   mobotMINI.right_motor.brake()

Complete beginner test
----------------------

.. code-block:: python

   import time

   print("Step 1: move")
   mobotMINI.left_motor.set_direction_and_speed(0, 50)
   mobotMINI.right_motor.set_direction_and_speed(0, 50)
   time.sleep(1.5)

   print("Step 2: pivot")
   mobotMINI.left_motor.set_direction_and_speed(0, 50)
   mobotMINI.right_motor.set_direction_and_speed(1, 50)
   time.sleep(1.0)

   print("Step 3: stop")
   mobotMINI.left_motor.stop()
   mobotMINI.right_motor.stop()

.. tip::
   Keep first tests in the ``40``-``60`` speed range.

.. warning::
   Lift wheels during first direction check for safety.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotMINI.left_motor.set_direction_and_speed(0, 50)
         mobotMINI.right_motor.set_direction_and_speed(0, 50)

   .. tab-item:: Full script

      .. code-block:: python

         import time
         mobotMINI.left_motor.set_direction_and_speed(0, 50)
         mobotMINI.right_motor.set_direction_and_speed(0, 50)
         time.sleep(1)
         mobotMINI.left_motor.stop()
         mobotMINI.right_motor.stop()

Common mistakes
---------------

- Expecting values above ``100`` to increase speed.
- Ignoring motor inversion config when direction seems reversed.
- Using abrupt full speed in first tests.
