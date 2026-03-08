Compass
=======

The compass provides heading information so your robot can keep or compare direction.

Important: this class expects calibration data. If not calibrated, ``read()`` raises
``RuntimeError``.

Main methods:

- ``calibrate(samples=100)``
- ``read()``
- ``turn_to_heading(target_deg, ..., L=left_motor, R=right_motor)``

Quick test
----------

.. code-block:: python

   # Run once when needed to generate calibration file
   # mobotROBOTICS.compass.calibrate(samples=100)

   heading = mobotROBOTICS.compass.read()
   print("Heading:", heading)

Heading change check
--------------------

.. code-block:: python

   first = mobotROBOTICS.compass.read()
   print("Heading A:", first)

   # Rotate robot manually, then read again
   second = mobotROBOTICS.compass.read()
   print("Heading B:", second)

   if first != second:
       print("Heading changed")

Turn to target heading example
------------------------------

.. code-block:: python

   target = 90
   print("Turning to", target, "degrees")

   mobotROBOTICS.compass.turn_to_heading(
      target_deg=target,
      base_speed=28,
      kp=0.8,
      tol_deg=5,
      timeout_s=8,
      L=mobotROBOTICS.left_motor,
      R=mobotROBOTICS.right_motor,
   )

   print("Turn complete")

.. warning::
   Run calibration in the real operating environment before relying on heading accuracy.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         print(mobotROBOTICS.compass.read())

   .. tab-item:: Full script

      .. code-block:: python

         # One-time calibration (uncomment when needed)
         # mobotROBOTICS.compass.calibrate(samples=100)

         heading = mobotROBOTICS.compass.read()
         print("Heading:", heading)

Common mistakes
---------------

- Calling ``read()`` before calibration file exists.
- Calibrating near strong magnets or power supplies.
- Expecting perfect heading without filtering/noise handling.
