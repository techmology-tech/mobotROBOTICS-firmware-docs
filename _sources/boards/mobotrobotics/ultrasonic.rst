Ultrasonic Sensor
=================

The ultrasonic sensor measures distance to objects in front of the robot (in centimeters).

This is commonly used for obstacle avoidance.

Quick test
----------

.. code-block:: python

   distance_cm = mobotROBOTICS.ultrasonic.get_distance_cm()
   print("Distance:", distance_cm, "cm")

Obstacle-stop example
---------------------

.. code-block:: python

   distance_cm = mobotROBOTICS.ultrasonic.get_distance_cm()
   print("Distance:", distance_cm, "cm")

   if distance_cm < 20:
       print("Obstacle too close -> stop motors")
       mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 0)
       mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 0)
   else:
       print("Path is clear")

Detection helper
----------------

.. code-block:: python

   if mobotROBOTICS.ultrasonic.is_object_detected(threshold_cm=15):
       print("Object detected within 15 cm")
   else:
       print("No close object")

.. warning::
    Keep a clear front path during testing to avoid sudden stops.

Example
-------

.. tab-set::

    .. tab-item:: Quick test

        .. code-block:: python

            print(mobotROBOTICS.ultrasonic.get_distance_cm())

    .. tab-item:: Full script

        .. code-block:: python

            import time

            for _ in range(10):
                 d = mobotROBOTICS.ultrasonic.get_distance_cm()
                 print("Distance:", d)
                 time.sleep(0.2)

Common mistakes
---------------

- Treating ``-1`` as valid distance (it means out-of-range/error).
- Comparing floats without handling noisy values.
- Mounting sensor at an angle and expecting stable readings.
