IR Sensors
==========

The IR sensor array is used for line tracking and near-obstacle detection.

Main methods:

- ``readSingleIR(index)``
- ``readAllIRs()``
- ``compIRs(expected_list)``

Each value is digital (typically ``0`` or ``1`` depending on wiring/sensor logic).

Quick test
----------

.. code-block:: python

   print("Reading IR sensors...")
   values = mobotROBOTICS.irs.readAllIRs()
   print("IR values:", values)

Simple line-following decision example
--------------------------------------

.. code-block:: python

   values = mobotROBOTICS.irs.readAllIRs()
   print("IR:", values)

   # Example strategy (adapt indices/thresholds to your sensor layout)
   if values[0] and not values[-1]:
      print("Line is on left -> turn left")
   elif values[-1] and not values[0]:
      print("Line is on right -> turn right")
   else:
      print("Keep moving forward")

.. note::
   Sensor logic can be inverted depending on module/wiring. Validate with printed values.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         print(mobotROBOTICS.irs.readAllIRs())

   .. tab-item:: Full script

      .. code-block:: python

         import time

         for _ in range(10):
             vals = mobotROBOTICS.irs.readAllIRs()
             print("IR:", vals)
             time.sleep(0.1)

Common mistakes
---------------

- Using ``read()`` instead of ``readAllIRs()``.
- Hardcoding thresholds/indices without reading actual values first.
- Forgetting sensor logic may be inverted.
