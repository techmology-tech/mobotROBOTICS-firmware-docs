LEDs
====

Mobot MINI provides two status LEDs:

- ``mobotMINI.led1``
- ``mobotMINI.led2``

Use LEDs to show states like ready, moving, waiting, and warning.

What you can control
--------------------

Each LED supports:

- ``on()`` / ``off()``
- ``toggle()``
- ``setState(state)`` where ``0`` is off and non-zero is on
- ``setLedBrightness(percent)`` where ``percent`` is clamped to ``0..100``

Quick test
----------

.. code-block:: python

   print("READY state")
   mobotMINI.led1.on()
   mobotMINI.led2.off()

Brightness example
------------------

.. code-block:: python

   print("Set soft brightness")
   mobotMINI.led1.setLedBrightness(20)

   print("Set strong brightness")
   mobotMINI.led2.setLedBrightness(85)

Pattern example
---------------

.. code-block:: python

   import time

   for step in range(4):
       print("Pattern step", step + 1)
       mobotMINI.led1.toggle()
       mobotMINI.led2.toggle()
       time.sleep(0.2)

.. note::
   Brightness values are clamped to ``0..100``.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotMINI.led1.setLedBrightness(25)
         mobotMINI.led2.setLedBrightness(75)

   .. tab-item:: Full script

      .. code-block:: python

         import time
         mobotMINI.led1.on()
         time.sleep(0.3)
         mobotMINI.led1.off()
         mobotMINI.led2.on()

Common mistakes
---------------

- Forgetting LED objects may be ``None`` if init failed.
- Passing non-numeric values to ``setLedBrightness``.
- Expecting ``setState(0)`` to dim instead of turn fully off.
