Servo
=====

Servos let you move parts to a target angle (for example: arm, gripper, pointer).

Initialize once with ``mobotROBOTICS.init_servo()``. After that:

- ``mobotROBOTICS.servo1`` ... ``mobotROBOTICS.servo4`` are available
- ``mobotROBOTICS.servo`` is an alias of ``servo1``
- each servo object supports ``move(angle)``, ``center()``, ``off()``

Quick test
----------

.. code-block:: python

   print("Init servo system")
   mobotROBOTICS.init_servo()

   # Move servo1 to 90°
   mobotROBOTICS.servo1.move(90)
   print("servo1 moved to 90°")

Angle sweep example
-------------------

.. code-block:: python

   import time

   mobotROBOTICS.init_servo()

   print("Go to 45")
   mobotROBOTICS.servo1.move(45)
   time.sleep(0.8)

   print("Go to 90")
   mobotROBOTICS.servo1.center()
   time.sleep(0.8)

   print("Go to 135")
   mobotROBOTICS.servo1.move(135)

   print("Disable servo signal when done")
   mobotROBOTICS.servo1.off()

.. warning::
   Always initialize servos first with ``mobotROBOTICS.init_servo()``.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotROBOTICS.init_servo()
         mobotROBOTICS.servo1.center()

   .. tab-item:: Full script

      .. code-block:: python

         import time
         mobotROBOTICS.init_servo()

         for angle in (45, 90, 135):
             mobotROBOTICS.servo1.move(angle)
             time.sleep(0.6)

         mobotROBOTICS.servo1.off()

Common mistakes
---------------

- Using ``servo.write(...)`` instead of ``move(...)``/``center()``.
- Forgetting to initialize servo channels.
- Forcing mechanical limits beyond safe angle range.
