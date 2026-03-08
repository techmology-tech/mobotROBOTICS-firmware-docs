BLE
===

The ``mobotROBOTICS.ble`` object is the wireless bridge between your robot and the app.
In practice, you use it to:

- Read control input (joystick/buttons)
- Track connection/state values
- Change robot BLE settings
- Send sensor telemetry back to the app

Read-only properties (snapshot values)
--------------------------------------

- ``x`` and ``y`` joystick values (range ``-128`` to ``127``)
- ``isPressed`` dictionary with keys: ``a``, ``b``, ``x``, ``y``, ``up``, ``down``, ``left``, ``right``
- ``mobot_name``
- ``control_mode``
- ``motor_config``
- ``battery_level``
- ``is_connected``
- ``is_running``
- ``is_ble_on``
- ``ir_sensors`` (telemetry snapshot object)
- ``ultrasonic_distance``
- ``color_sensor`` (telemetry snapshot object)

Quick property read
-------------------

.. code-block:: python

   print("x:", mobotROBOTICS.ble.x, "y:", mobotROBOTICS.ble.y)
   print("connected:", mobotROBOTICS.ble.is_connected)
   print("mode:", mobotROBOTICS.ble.control_mode)
   print("battery:", mobotROBOTICS.ble.battery_level)

   buttons = mobotROBOTICS.ble.isPressed
   print("A:", buttons["a"], "B:", buttons["b"], "UP:", buttons["up"])

Pop methods (read-and-clear)
----------------------------

- ``pop_gamepad()`` -> ``(x, y, buttons)`` or ``None``
- ``pop_control_mode_changed()`` -> ``bool``
- ``pop_motor_config_changed()`` -> ``bool``

.. code-block:: python

   event = mobotROBOTICS.ble.pop_gamepad()
   if event is None:
       print("No new gamepad input yet")
   else:
       x, y, buttons = event
       print("x=", x, "y=", y, "buttons=", buttons)

Snapshot + callbacks
--------------------

- ``get_state_snapshot()``
- ``on_mode_change(callback)``
- ``on_config_change(callback)``

.. code-block:: python

   def on_mode(old_mode, new_mode):
       print("Mode changed:", old_mode, "->", new_mode)

   mobotROBOTICS.ble.on_mode_change(on_mode)
   print(mobotROBOTICS.ble.get_state_snapshot())

Control and configuration methods
---------------------------------

- ``changeName(name)``
- ``set_control_mode(mode)``
- ``set_battery_level(level)``

.. code-block:: python

   mobotROBOTICS.ble.changeName("Mobot ROBOTICS")
   mobotROBOTICS.ble.set_control_mode(0)
   mobotROBOTICS.ble.set_battery_level(90)

Telemetry setter methods
------------------------

- ``set_ir_sensors(raw)`` or ``set_ir_sensors(s0, s1, s2, s3, s4)``
- ``set_ultrasonic_distance(distance_cm)``
- ``set_color_sensor(r, g, b, intensity=0)``

.. code-block:: python

   ir_values = mobotROBOTICS.irs.readAllIRs()
   dist = mobotROBOTICS.ultrasonic.get_distance_cm()
   r, g, b, clear = mobotROBOTICS.color_sensor.readColor()

   mobotROBOTICS.ble.set_ir_sensors(*ir_values)
   mobotROBOTICS.ble.set_ultrasonic_distance(int(dist))
   mobotROBOTICS.ble.set_color_sensor(r, g, b, clear)

Activation gate methods
-----------------------

- ``enable_activation_gate(enabled=True)``
- ``is_activation_gate_enabled()``
- ``is_activated()``

.. code-block:: python

   mobotROBOTICS.ble.enable_activation_gate(True)
   print("Gate enabled:", mobotROBOTICS.ble.is_activation_gate_enabled())
   print("Activated now:", mobotROBOTICS.ble.is_activated())

Background lifecycle methods
----------------------------

- ``start_ble_background()``
- ``stop_ble_background(timeout_ms=3000)``
- ``shutdown_ble_thread(timeout_ms=1000)``

.. code-block:: python

   mobotROBOTICS.ble.start_ble_background()
   print("BLE running:", mobotROBOTICS.ble.is_running)

Helper conversion methods
-------------------------

- ``mode_to_string(mode)``
- ``event_to_string(event)``
- ``error_to_string(error)``

.. code-block:: python

   print(mobotROBOTICS.ble.mode_to_string(0))
   print(mobotROBOTICS.ble.event_to_string(2))
   print(mobotROBOTICS.ble.error_to_string(1))

.. note::
   Prefer ``pop_*`` methods for event-driven loops to avoid reprocessing stale inputs.

.. warning::
   Avoid repeatedly starting/stopping BLE thread in tight loops.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         print("Connected:", mobotROBOTICS.ble.is_connected)
         print("Gamepad:", mobotROBOTICS.ble.pop_gamepad())

   .. tab-item:: Full script

      .. code-block:: python

         import time

         mobotROBOTICS.ble.start_ble_background()
         while True:
             event = mobotROBOTICS.ble.pop_gamepad()
             if event:
                 print("Event:", event)
             time.sleep(0.05)

Common mistakes
---------------

- Reading only ``x``/``y`` and forgetting button states from ``isPressed``.
- Not handling ``None`` result from ``pop_gamepad()``.
- Sending telemetry with wrong value shapes (e.g., bad IR arg count).
