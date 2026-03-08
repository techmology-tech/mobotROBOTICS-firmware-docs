Mobot User Guide
================

Welcome! This guide is written for learners, students, and makers using Mobot boards
with MicroPython.

If you just bought your robot, start by choosing your board below. Each board page has:

- A simple overview
- Clear component-by-component pages
- Ready-to-run code snippets

.. toctree::
   :maxdepth: 2
   :caption: Boards

   boards/index

First control example
---------------------

.. code-block:: python

   # Mobot ROBOTICS
   mobotROBOTICS.left_motor.setDirectionAndSpeed(1, 80)

   # Mobot MINI
   mobotMINI.left_motor.set_direction_and_speed(1, 80)
