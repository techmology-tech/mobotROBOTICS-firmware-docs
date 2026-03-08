Motors
======

Mobot ROBOTICS has **two DC motors**:

- ``mobotROBOTICS.left_motor`` controls the left wheel
- ``mobotROBOTICS.right_motor`` controls the right wheel

You choose movement by setting **direction** and **speed** for each motor.

Direction
---------

Direction is selected with the first argument:

- ``0``: one rotation direction
- ``1``: opposite rotation direction

If your robot goes backward when you expect forward, switch ``0`` and ``1`` in your code.

Speed (percent)
---------------

Speed is the second argument and is a percentage:

- ``0`` = stopped
- ``100`` = full speed
- ``50`` = half speed

Most beginner tests work well in the ``40`` to ``70`` range.

Quick test
----------

.. code-block:: python

   print("Move both motors at 60%...")

   # direction, speed_percent
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 60)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 60)

   print("Robot should now move in a straight line")

Turn in place
-------------

.. code-block:: python

   print("Turn right in place")

   # Left wheel forward-like direction, right wheel opposite direction
   # Same speed on both sides -> cleaner pivot
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 55)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(0, 55)

   print("If turn direction is opposite, swap 0 and 1")

Complete beginner test
----------------------

.. code-block:: python

   import time

   print("Step 1: forward test")
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 50)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 50)
   time.sleep(1.5)

   print("Step 2: turn test")
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 50)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(0, 50)
   time.sleep(1.0)

   print("Step 3: stop")
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 0)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 0)

.. tip::
   Start with ``40``-``60`` speed for first tests to reduce sudden movement.

.. warning::
   Lift wheels off the ground during first direction tests to avoid accidental runaways.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 50)
         mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 50)

   .. tab-item:: Full script

      .. code-block:: python

         import time

         print("Forward")
         mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 50)
         mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 50)
         time.sleep(1)

         print("Stop")
         mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 0)
         mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 0)

Common mistakes
---------------

- Using speed above ``100`` and expecting more power (values are clamped).
- Assuming ``0`` always means forward on every wiring setup.
- Testing high speed before confirming direction safely.
