Buzzer
======

The buzzer gives audio feedback for startup, warnings, and user actions.

Buzzer object: ``mobotMINI.buzzer``.

What you can control
--------------------

- ``play(song_string, looping=True)``
- ``stop()`` / ``pause()`` / ``resume()``
- ``is_playing()``
- ``get_current_song()``
- ``set_tempo(value)`` (higher value = slower)
- ``set_volume(duty)``

Quick test
----------

.. code-block:: python

   from indicators import SONGS

   print("Play startup tone once")
   mobotMINI.buzzer.play(SONGS["startup"], looping=False)

Playback control example
------------------------

.. code-block:: python

   print("Is playing:", mobotMINI.buzzer.is_playing())

   print("Pause")
   mobotMINI.buzzer.pause()

   print("Resume")
   mobotMINI.buzzer.resume()

   print("Stop")
   mobotMINI.buzzer.stop()

Custom song example
-------------------

.. code-block:: python

   # Format: "<beat> <note> <duration> <channel>"
   # Notes separated by semicolons
   short_song = "0 C4 2 0;2 E4 2 0;4 G4 2 0"

   print("Play custom song")
   mobotMINI.buzzer.play(short_song, looping=False)

.. tip::
   Keep short non-looping tones for user feedback events.

Example
-------

.. tab-set::

   .. tab-item:: Quick test

      .. code-block:: python

         from indicators import SONGS
         mobotMINI.buzzer.play(SONGS["startup"], looping=False)

   .. tab-item:: Full script

      .. code-block:: python

         mobotMINI.buzzer.set_tempo(3)
         mobotMINI.buzzer.play("0 C4 2 0;2 E4 2 0", looping=False)
         print("Playing:", mobotMINI.buzzer.is_playing())

Common mistakes
---------------

- Assuming ``play`` blocks until melody finishes.
- Forgetting to call ``stop()`` during mode changes.
- Using malformed song string format.
