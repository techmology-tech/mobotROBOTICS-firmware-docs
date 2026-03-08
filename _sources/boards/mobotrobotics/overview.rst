Mobot ROBOTICS Overview
=======================

Welcome to **Mobot ROBOTICS** 🎉

When your board starts, the ``mobotROBOTICS`` object is already available. This means
you can begin writing robot code right away without extra setup imports.

What you can control
--------------------

- Motors for movement
- Servo outputs
- BLE controller data
- LEDs and buzzer feedback
- Sensors (IR, ultrasonic, color, compass, joysticks)

Explore by component
--------------------

.. toctree::
   :maxdepth: 1

   leds
   buzzer
   motors
   ir_sensors
   ultrasonic
   color_sensor
   compass
   joysticks
   servo
   ble

Your first movement command
---------------------------

.. code-block:: python

   # Reverse direction (1) at 80% speed
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 80)
   mobotROBOTICS.right_motor.setDirectionAndSpeed(1, 80)

