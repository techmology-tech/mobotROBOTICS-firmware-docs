Joysticks
=========

Joystick objects let you read manual input values (for teleoperation and testing).

Available joystick objects:

- ``mobotROBOTICS.joystick1``
- ``mobotROBOTICS.joystick2``

Quick test
----------

.. code-block:: python

   print("Initialize joystick subsystem")
   mobotROBOTICS.init_joysticks()

   j1x = mobotROBOTICS.joystick1.readX()
   j1y = mobotROBOTICS.joystick1.readY()
   j2x = mobotROBOTICS.joystick2.readX()
   j2y = mobotROBOTICS.joystick2.readY()
   print("J1:", (j1x, j1y), "J2:", (j2x, j2y))

Continuous read example
-----------------------

.. code-block:: python

   import time

   mobotROBOTICS.init_joysticks()
   print("Reading joystick values for 5 iterations")

   for _ in range(5):
       j1 = (mobotROBOTICS.joystick1.readX(), mobotROBOTICS.joystick1.readY())
       j2 = (mobotROBOTICS.joystick2.readX(), mobotROBOTICS.joystick2.readY())
       print("J1:", j1, "| J2:", j2)
       time.sleep(0.2)

Simple speed mapping idea
-------------------------

.. code-block:: python

   # ADC values are around 0..1023 (10-bit)
   y = mobotROBOTICS.joystick1.readY()

   # Map to 0..100 speed (example)
   speed_percent = int((y / 1023) * 100)
   print("Mapped speed %:", speed_percent)

.. tip::
   Observe center values first; analog joysticks often do not center at exactly the same raw number.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotROBOTICS.init_joysticks()
         print(mobotROBOTICS.joystick1.readX(), mobotROBOTICS.joystick1.readY())

   .. tab-item:: Full script

      .. code-block:: python

         import time
         mobotROBOTICS.init_joysticks()

         for _ in range(20):
             x = mobotROBOTICS.joystick1.readX()
             y = mobotROBOTICS.joystick1.readY()
             print("J1:", x, y)
             time.sleep(0.05)

Common mistakes
---------------

- Using ``read()`` instead of ``readX()``/``readY()``.
- Forgetting ``init_joysticks()`` before first access.
- Mapping raw values directly to motors without deadzone.
