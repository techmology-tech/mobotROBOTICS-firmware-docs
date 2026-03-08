LEDs
====

Mobot ROBOTICS exposes two LEDs:

- ``mobotROBOTICS.led1``
- ``mobotROBOTICS.led2``

Use them to show state (ready, running, warning, etc.).

Each LED supports:

- ``on()`` / ``off()``
- ``setState(state)`` where ``0`` is off and non-zero is on
- ``setLedBrightness(percent)`` where percent is clamped to ``0..100``

Quick test
----------

.. code-block:: python

   print("Show READY state")
   mobotROBOTICS.led1.on()
   mobotROBOTICS.led2.off()

Brightness control
------------------

.. code-block:: python

   print("Set LED1 to 25% brightness")
   mobotROBOTICS.led1.setLedBrightness(25)

   print("Set LED2 to 80% brightness")
   mobotROBOTICS.led2.setLedBrightness(80)

Simple blink pattern
--------------------

.. code-block:: python

   import time

   for i in range(3):
       print("Blink", i + 1)
       mobotROBOTICS.led1.on()
       mobotROBOTICS.led2.off()
       time.sleep(0.25)
       mobotROBOTICS.led1.off()
       mobotROBOTICS.led2.on()
       time.sleep(0.25)

.. note::
   ``setLedBrightness(percent)`` clamps values outside ``0..100``.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotROBOTICS.led1.setLedBrightness(30)
         mobotROBOTICS.led2.setLedBrightness(80)

   .. tab-item:: Full script

      .. code-block:: python

         import time

         mobotROBOTICS.led1.on()
         mobotROBOTICS.led2.off()
         time.sleep(0.4)
         mobotROBOTICS.led1.off()
         mobotROBOTICS.led2.on()

Common mistakes
---------------

- Calling LED methods before ``mobotROBOTICS.init()`` has run.
- Expecting negative brightness values to dim differently.
- Forgetting to turn off LEDs in long-running scripts.
