Processes
=========

.. _starting:

Starting the T&E
-----------------

1. In the Anemies room, press the start demo button on the screen. 

Troubleshooting
^^^^^^^^^^^^^^^
**fix 1**: If the screen in the Anemies room is black, unplug the single board computers (SBCs) and plug them in again. The startup program should start automatically. 

**fix 2**: If the screen is still black or if pushing the start button does not work, Remove the smart plugs and plug in every single board computer of the T&E Center. 
The SBCs will switch on and the dems starts automatically. 

**fix 3**:If the demos don't start when the SBC is swithced on, double click on the desktop icon corresponding to the demo of the stand.

.. _stopping:

Stopping the T&E
-----------------

In the Anemones room, press the stop demo button on the screen. If the SBC is off, plug it in and the program should start automatically.

Troubleshooting
^^^^^^^^^^^^^^^

**fix 1**: If the demo don't switch off when the stop button is pressed, unplug every SBCs of the T&E Center.

.. _adding:

Adding a Demo
-------------

1. Configure a new SBC (see above)
2. Create a new ``name_of_the_demo.sh``
3. Run the script ``add_demo.sh`` to add a desktop link with the new demo to all SBCs
