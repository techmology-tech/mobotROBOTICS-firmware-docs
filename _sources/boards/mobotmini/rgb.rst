RGB LED
=======

Mobot MINI includes a WS2812 RGB LED at ``mobotMINI.rgb``.

Use it for visual feedback: mode colors, warnings, and effects.

What you can control
--------------------

- ``set_color(r, g, b, index=0)``
- ``set_hex(hex_color, index=0)``
- ``set_brightness(percent)`` (``0..100``)
- ``set_preset(preset_id)``
- ``flash(r, g, b, duration_ms=50)``
- ``off()``
- ``get_color(index=0)``
- ``get_brightness()``

Quick test
----------

.. code-block:: python

   print("Green ready color")
   mobotMINI.rgb.set_color(0, 255, 0)

Brightness + preset example
---------------------------

.. code-block:: python

   print("Lower brightness to 30%")
   mobotMINI.rgb.set_brightness(30)

   print("Apply blue preset")
   mobotMINI.rgb.set_preset(0x03)

Flash warning example
---------------------

.. code-block:: python

   print("Flash red warning")
   mobotMINI.rgb.flash(255, 0, 0, duration_ms=120)

Readback example
----------------

.. code-block:: python

   color = mobotMINI.rgb.get_color()
   brightness = mobotMINI.rgb.get_brightness()
   print("Current color:", color)
   print("Brightness:", brightness)

.. warning::
   Avoid maximum brightness for long periods on battery power.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotMINI.rgb.set_preset(0x03)

   .. tab-item:: Full script

      .. code-block:: python

         import time
         mobotMINI.rgb.set_brightness(30)
         mobotMINI.rgb.set_color(0, 255, 0)
         time.sleep(0.5)
         mobotMINI.rgb.flash(255, 0, 0, duration_ms=120)

Common mistakes
---------------

- Using color values outside ``0..255`` and expecting overflow behavior.
- Forgetting brightness scaling affects perceived color intensity.
- Assuming preset IDs outside map are valid.
