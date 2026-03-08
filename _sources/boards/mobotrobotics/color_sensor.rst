Color Sensor
============

Use the color sensor to read detected color information for sorting or reactions.

Main methods:

- ``readColor()`` -> returns color tuple (for example ``r, g, b, clear``)
- ``printColors()``
- ``compColor(rgb, target_color, th=20)`` for threshold comparison

Quick test
----------

.. code-block:: python

   print("Read color sensor...")
   r, g, b, clear = mobotROBOTICS.color_sensor.readColor()
   print("R:", r, "G:", g, "B:", b, "Clear:", clear)

Simple reaction example
-----------------------

.. code-block:: python

   rgb = mobotROBOTICS.color_sensor.readColor()
   print("Color data:", rgb)

   # Compare measured color to target red-like value
   is_red_like = mobotROBOTICS.color_sensor.compColor(rgb, (200, 40, 40), th=40)
   print("Looks red:", is_red_like)

.. tip::
   Recalibrate expected color targets under your actual lighting conditions.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         print(mobotROBOTICS.color_sensor.readColor())

   .. tab-item:: Full script

      .. code-block:: python

         import time

         for _ in range(10):
             rgb = mobotROBOTICS.color_sensor.readColor()
             print("RGBC:", rgb)
             time.sleep(0.2)

Common mistakes
---------------

- Expecting stable values when ambient light changes.
- Using too strict threshold in ``compColor``.
- Forgetting returned tuple may include intensity/clear channel.
