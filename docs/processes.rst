Processes
=========

.. _starting:

Starting the T&E
-----------------
As exlained in the :ref:`architecture`, each single board computer is connected through the electricity network through a smart plug. 
When the smart plug is turned on, the SBC is powered on and the demos automatically start thanks to its startup script (see :ref:`scripts`)
The smart plugs are scheduled to power on at 9:00 am and power off at 6:00 pm in the week. If you wish to start the T&E outside of these hours, follow the steps below.
1. Connect to the [shelly mobile](https://play.google.com/store/apps/details?id=cloud.shelly.smartcontrol&hl=en_US) or [web app](https://control.shelly.cloud/) with the experience center credentials.
2. Navigate to the experience center room, then to groups and click the on button. 
3. If you wich to start only one demo, navigate to the corresponding plug and click on the on button.

   
Troubleshooting
^^^^^^^^^^^^^^^

In case of power outage, the plugs take a few minutes to reconnect to the wifi. If you wich to turn everything back on more rapidly, follow the steps below.
1. Click on the side button of each smart plug to turn them on. 

.. _stopping:

Stopping the T&E
-----------------
The smart plugs are scheduled to power on at 9:00 am and power off at 6:00 pm in the week. If you wish to start the T&E outside of these hours, follow the steps below.
1. Connect to the shelly mobile or web app with the experience center credentials.
2. Navigate to the experience center room, then to groups and click the off button. 
3. If you wich to stop only one demo, navigate to the corresponding plug and click on the off button.


Adding a Demo
-------------

1. Configure a new SBC (see above)
2. Create a new ``name_of_the_demo.sh``
3. Run the script ``add_demo.sh`` to add a desktop link with the new demo to all SBCs



