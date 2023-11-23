.. _processes:
Processes
=========

.. _starting:

Starting the T&E
-----------------
As exlained in the :ref:`architecture`, each single board computer is connected through the electricity network through a smart plug. 
When the smart plug is turned on, the SBC is powered on and the demos automatically start thanks to its startup script (see :ref:`scripts`)
The smart plugs are scheduled to power on at 9:00 am and power off at 6:00 pm in the week. If you wish to start the T&E outside of these hours, follow the steps below.

1. Connect to the `shelly mobile <https://play.google.com/store/apps/details?id=cloud.shelly.smartcontrol&hl=en_US>`_ or `web app <https://control.shelly.cloud/>`_ with the experience center credentials.
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

1. Flash a new SBC with one of the fari custom image. or create a new distribition as descibed in the :ref:`sbc` section.
2. If you plug the SBC to a new socket (that has no smart plug yet), you need to plug a new smart plug the the socket and add it the the test and experience center room and the demo group in the shelly app.
3. Clone the `TE-Scripts repository <https://github.com/FARI-brussels/TE-Scripts>`_ in the documents.
4. Create a new script ``name_of_the_demo.sh`` in the ``individual_demos`` folder of the `TE-Scripts repository <https://github.com/FARI-brussels/TE-Scripts>`_ 
   Here is the minimal content of this script:
.. code-block:: bash

    DEMO_ID="CMS_ID"
    WELCOME_SCREEN_DIR="/home/fari/Documents/Welcome-Screen"
    WELCOME_SCREEN_REPO="https://github.com/FARI-brussels/welcome-screen"
    SCRIPT_DIR="/home/fari/Documents/TE-Scripts"

    # Use git_sync.sh to sync both repositories
    "$SCRIPT_DIR/clone_or_pull_repo.sh" "$WELCOME_SCREEN_DIR" "$WELCOME_SCREEN_REPO"

    # Launch the welcome screen using launch_welcome_screen.sh
    "$SCRIPT_DIR/launch_welcome_screen.sh" "$WELCOME_SCREEN_DIR" "$DEMO_ID"

If the demo relies on additional code, you can add it to the script.

5. Make the script executable with the following command:
   
.. code-block:: bash

    chmod +x name_of_the_demo.sh
1. On the SBC desktop, go to startup applications and add a new startup program with the following command:
   
.. code-block:: bash  

    bash /home/fari/Documents/TE-Scripts/individual_demos/name_of_the_demo.sh

