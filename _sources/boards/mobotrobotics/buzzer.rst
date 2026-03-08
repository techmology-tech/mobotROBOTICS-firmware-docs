Buzzer
======

Use the buzzer to provide immediate sound feedback for users.

Typical uses:

- Startup confirmation
- Error alerts
- Action complete notifications

The buzzer object is ``mobotROBOTICS.buzzer`` (``BuzzerPlayer``).
Useful methods:

- ``play(song_string, looping=True)``
- ``stop()``, ``pause()``, ``resume()``
- ``is_playing()``, ``get_current_song()``
- ``set_tempo(value)``, ``set_volume(duty)``

Quick test
----------

.. code-block:: python

   from indicators import SONGS

   print("Play startup sound once")
   mobotROBOTICS.buzzer.play(SONGS["startup"], looping=False)

Custom tune example
-------------------

.. code-block:: python

   # Format: "<beat> <note> <duration> <channel>"
   # Notes are separated by semicolons
   short_tune = "0 C4 2 0;2 E4 2 0;4 G4 2 0"

   print("Play custom tune")
   mobotROBOTICS.buzzer.play(short_tune, looping=False)

Playback state check
--------------------

.. code-block:: python

   print("Playing:", mobotROBOTICS.buzzer.is_playing())
   print("Current song:", mobotROBOTICS.buzzer.get_current_song())

   print("Pause")
   mobotROBOTICS.buzzer.pause()

   print("Resume")
   mobotROBOTICS.buzzer.resume()

   print("Stop")
   mobotROBOTICS.buzzer.stop()

.. tip::
   Use ``looping=False`` for short feedback sounds.

.. warning::
   Very frequent high-volume playback can be annoying in classroom environments.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         mobotROBOTICS.buzzer.play("0 C4 2 0;2 E4 2 0", looping=False)

   .. tab-item:: Full script

      .. code-block:: python

         from indicators import SONGS

         mobotROBOTICS.buzzer.set_tempo(3)
         mobotROBOTICS.buzzer.play(SONGS["startup"], looping=False)
         print("Playing:", mobotROBOTICS.buzzer.is_playing())

Common mistakes
---------------

- Assuming ``play`` blocks execution (it is non-blocking).
- Forgetting to call ``stop()`` when changing activity modes.
- Passing malformed song strings.
