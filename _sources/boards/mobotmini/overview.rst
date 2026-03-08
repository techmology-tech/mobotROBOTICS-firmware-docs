Mobot MINI Overview
===================

Welcome to **Mobot MINI**.

At startup, your board gives you a ready-to-use ``mobotMINI`` object, so you can go
straight to motor control, BLE input, and status indicators.

What you can do quickly
-----------------------

- Drive using left and right motors
- Read controls from BLE
- Show status with dedicated LED and RGB control
- Play feedback sounds with the buzzer

Explore by component
--------------------

.. toctree::
   :maxdepth: 1

   leds
   buzzer
   motors
   rgb
   ble

Your first movement command
---------------------------

.. code-block:: python

   print("Move forward at 80%")
   mobotMINI.left_motor.set_direction_and_speed(1, 80)
   mobotMINI.right_motor.set_direction_and_speed(1, 80)

