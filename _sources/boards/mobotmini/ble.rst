BLE
===

Use ``mobotMINI.ble`` to read phone/controller input and robot state.

This object is typically used for:

- Checking whether the robot is connected
- Reading gamepad/joystick events
- Managing BLE background handling

Main properties
---------------

- ``x``, ``y`` joystick values
- ``isPressed`` dictionary (``a``, ``b``, ``x``, ``y``, ``up``, ``down``, ``left``, ``right``)
- ``is_connected``, ``is_running``, ``is_ble_on``
- ``mobot_name``, ``control_mode``, ``battery_level``
- ``motor_config``
- ``rgb_color_mode``
- ``piano_input``
- ``action_sequence_control``

Quick property read
-------------------

.. code-block:: python

   print("x:", mobotMINI.ble.x, "y:", mobotMINI.ble.y)
   print("connected:", mobotMINI.ble.is_connected)
   print("mode:", mobotMINI.ble.control_mode)
   print("battery:", mobotMINI.ble.battery_level)

   pressed = mobotMINI.ble.isPressed
   print("A:", pressed["a"], "B:", pressed["b"], "UP:", pressed["up"])

Read controller input
---------------------

.. code-block:: python

   event = mobotMINI.ble.pop_gamepad()
   if event is None:
       print("No new input")
   else:
       x, y, buttons = event
       print("Gamepad event:", x, y, buttons)

Common pop methods
------------------

- ``pop_gamepad()``
- ``pop_control_mode_changed()``
- ``pop_motor_config_changed()``

MINI-specific pop methods
-------------------------

Use these when your app sends MINI-specific commands:

- ``pop_rgb_color_mode_changed()`` -> ``(changed, value)``
- ``pop_action_sequence()`` -> ``(changed, data_bytes)``
- ``pop_action_sequence_control()`` -> ``(changed, control)``
- ``pop_piano_input()`` -> ``(changed, bitmask)``

.. code-block:: python

   changed, preset = mobotMINI.ble.pop_rgb_color_mode_changed()
   if changed:
       print("New RGB preset:", preset)

   changed, sequence_data = mobotMINI.ble.pop_action_sequence()
   if changed:
       print("Sequence bytes length:", len(sequence_data))

   changed, control = mobotMINI.ble.pop_action_sequence_control()
   if changed:
       print("Sequence control:", control)

   changed, piano_bits = mobotMINI.ble.pop_piano_input()
   if changed:
       print("Piano input bitmask:", piano_bits)

Snapshot + callbacks
--------------------

- ``get_state_snapshot()``
- ``on_mode_change(callback)``
- ``on_config_change(callback)``

.. code-block:: python

   def on_mode(old_mode, new_mode):
       print("Mode changed:", old_mode, "->", new_mode)

   mobotMINI.ble.on_mode_change(on_mode)
   print(mobotMINI.ble.get_state_snapshot())

BLE control helpers
-------------------

.. code-block:: python

   print("Rename device and start BLE task")
   mobotMINI.ble.changeName("Mobot MINI")
   mobotMINI.ble.set_control_mode(0)
   mobotMINI.ble.set_battery_level(95)
   mobotMINI.ble.start_ble_background()

Activation gate methods
-----------------------

- ``enable_activation_gate(enabled=True)``
- ``is_activation_gate_enabled()``
- ``is_activated()``

.. code-block:: python

   mobotMINI.ble.enable_activation_gate(True)
   print("Gate enabled:", mobotMINI.ble.is_activation_gate_enabled())
   print("Activated now:", mobotMINI.ble.is_activated())

Background lifecycle methods
----------------------------

- ``start_ble_background()``
- ``stop_ble_background(timeout_ms=3000)``
- ``shutdown_ble_thread(timeout_ms=1000)``

.. code-block:: python

   mobotMINI.ble.start_ble_background()
   print("BLE running:", mobotMINI.ble.is_running)

Helper conversion methods
-------------------------

- ``mode_to_string(mode)``
- ``event_to_string(event)``
- ``error_to_string(error)``

.. code-block:: python

   print(mobotMINI.ble.mode_to_string(0))
   print(mobotMINI.ble.event_to_string(2))
   print(mobotMINI.ble.error_to_string(1))

.. note::
   Use pop methods in loops to process only new events.

.. warning::
   Do not restart BLE background repeatedly inside fast loops.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         print("Connected:", mobotMINI.ble.is_connected)
         print("Gamepad:", mobotMINI.ble.pop_gamepad())

   .. tab-item:: Full script

      .. code-block:: python

         import time

         mobotMINI.ble.start_ble_background()
         while True:
             event = mobotMINI.ble.pop_gamepad()
             if event:
                 print("Event:", event)
             time.sleep(0.05)

Common mistakes
---------------

- Forgetting ``None`` handling in pop methods.
- Ignoring MINI-specific pop APIs for RGB/sequence/piano data.
- Setting invalid control mode values.

State snapshot example
----------------------

.. code-block:: python

   snapshot = mobotMINI.ble.get_state_snapshot()
   print("BLE snapshot:", snapshot)
