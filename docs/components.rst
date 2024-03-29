.. _components:
Components
==========

.. _sbc:

Single Board Computers
----------------------

We currently have three different Single Board Computers (SBCs): Odroid C4, Odroid N2, and Raspberry Pi 4. 
All models run Armbian version 22 or greater with the GNOME desktop environment. 
Custom Fari images for each SBC can be found at the provided link (ADD LINK!). 

⚠️ When you add a new SBC, please register its mac addres in the Content Management System (required for the scripts to work in case we don't have access to fixed local ips)

Setting Up a Fari image for a New SBC type
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To prepare a new SBC with the Armbian image, follow these steps:

1. Download the latest Armbian image with GNOME desktop from `here <https://www.armbian.com/download/?device_support=Supported>`_.
2. Use Balena Etcher or a similar tool to flash the image onto an SD card.
3. Insert the SD card into the SBC and power it on.
4. When prompted, set the root and user passwords to `fari.brussels` and choose `fari` as the username. Note: The default keyboard layout is QWERTY.
5. Select `bash` as the default shell.
6. During the initial setup, opt to skip Wi-Fi connection and locale generation (skip generation locales).
7. In settings - keyboard, change keyboard layout to belgian
8. Connect to the wifi

Initial System Update and Package Installation
``````````````````````````````````````````````

Run the following commands to update the system and install necessary packages:

.. code-block:: bash

   sudo apt update
   sudo apt upgrade -y
   sudo apt install -y python-is-python3 pip sshpass arp-scan jq dos2unix xdotool gnome-startup-applications

Repeat the update and upgrade commands to ensure all packages are up to date:

.. code-block:: bash

   sudo apt update
   sudo apt upgrade -y

Configuring Auto-login
``````````````````````

To enable auto-login, modify the `11-armbian.conf` file located in `/etc/lightdm/lightdm.conf.d`:

.. code-block:: bash

   cd /etc/lightdm/lightdm.conf.d
   sudo nano 11-armbian.conf

Add the following lines to the file:

.. code-block:: none

   autologin-user=fari
   autologin-user-timeout=0

Final file should look like that : 

.. code-block:: none

   [Seat:*]
   autologin-user=fari
   autologin-user-timeout=0
   user-session=xfce
   greeter-show-manual-login=false
   greeter-hide-users=false
   allow-guest=false

Optional Steps
``````````````

- **Node.js Installation**: Follow the instructions at [nodesource/distributions](https://github.com/nodesource/distributions) to install Node.js.

- **Generating SSH Key for GitHub**:

  1. Generate an SSH key without a passphrase: `ssh-keygen -o -t rsa -C "experience@fari.brussels"`
  2. Retrieve the public key: `cat /home/fari/.ssh/id_rsa.pub`
  3. Copy the key to the Fari Brussels GitHub account as detailed at [TheServerSide.com](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/GitHub-SSH-Key-Setup-Config-Ubuntu-Linux).

- **Preventing Kernel Updates**: List installed kernel images and hold the current one to prevent updates:

  .. code-block:: bash

     dpkg --list | grep linux-image
     sudo apt-mark hold linux-image-current-meson64

- **Create a flashable image from the distro**: To create a flashable image from the distro.
  Linux

  1. Run `sudo fdisk -l` to list the available disks and partitions. Find the disk that corresponds to the SD card (for example /dev/sda).
  2. Run `sudo dd if=/dev/sda of=~/path_where_you_want_to_save_the_image.img`
  3. Use `PiShrink <https://github.com/Drewsif/PiShrink>`_ to shrink the image : `sudo bash pishrink.sh ~/path_where_you_have_saved_the_image.img`.
  4. Compress with xy : `xz -v ~/path_where_you_have_saved_the_image.img`
  5. Upload the compressed image to the cloud
   
  Windows
  You can use `Win32 <https://win32diskimager.org/>`_ to create an image of the SD card.


.. autosummary::
   :toctree: generated

Computers
---------

Beside the SBCs, we also have computers for demo that requires more power. While ubuntu is preferred for all devices, we also have windows computers for some demos.
Computers run on windows 10. The main disadvantage of windows is that the :ref:`scripts` cannot be used.
To set up a new windows computer, you can install the following ISO on the computer: ADD link.
You will need to set up the bios so that the computer lights on when the power is activated through the smart plug (As explained `here <https://www.wintips.org/setup-computer-to-auto-power-on-after-power-outage/>`_. 
Then you will need to write a script to launch the demo and add that script to the start up apps.

.. _sp:

Smart Plugs
-----------

All demos are wired to electricity through shelly smart plugs. The documentation can be found `here <https://shelly-api-docs.shelly.cloud>`_.
To access the dashboard, you can download the `shelly mobile app <https://play.google.com/store/apps/details?id=cloud.shelly.smartcontrol&hl=en_US>`_ or access to the `web app <https://control.shelly.cloud/>`_.
The credentials can be found on the test and experience password vault.

.. autosummary::
   :toctree: generated



.. _cms:
Content Management System
-------------------------

The experience center CMS is based on strapi. The documentation can be found `here <https://strapi.io/documentation/developer-docs/latest/getting-started/introduction.html>`_.
It is currently hosted on Gandi and can be accessed `here <http://46.226.110.124:1337/admin/>`_. If you need access to the CMS, please contact Siméon Michel.
We will soon migrate the CMS to a Strapi cloud infrastructure and the documentation will be updated accordingly.

The content management system contains the following collections:

1. **demo** (en/fr/nl) : 
   Contains all the information about the demos for the welcome screen to work properly. 
   The welcome screen of each demo call to the CMS to retrieve the information about the demo and display it on the screen.

2. **device** : 
   Contain all the information about the different devices (SBCs, smart plugs, etc.). This is useful for the :ref:`scripts` to work properly.
   It is mainly used to be able to retreive the local ip adress of the device if it has changed. If you add a new device you should register it there.

3. **Interface components** (en/fr/nl) : 
   Contains the multilingual content of the different interface components shared between different demos (buttons, titles, etc.)

4. **whichContentIsReal_MediaLists** : 
   This collection is used by the which content is real demo. It contains the different real/fake media pairs

5. **demo_chatbot** (en/fr/nl) : 
   This collection is used by the which content is real demo. It contains information about the different chatbot that can be used


You can connect to the server hosting the CMS using ssh : 
   .. code-block:: bash
      ssh fari@46.226.110.124

To prevent the CMS to shut down when exiting the terminal we use [pm2](https://pm2.keymetrics.io/) to launch the process.
   .. code-block:: bash
      #Start the cms
      pm2 start server

   .. code-block:: bash
      #Stop the cms
      pm2 stop server

When you want to add a new content type to the cms, it has to be launched using the following command :
   .. code-block:: bash
      cd fariCMS
      npm run develop

.. _welcome_screen:
Welcome Screen
--------------
Each demo is displayed on a screen with a welcome screen. The welcome screen is a web page that is displayed on a chromium browser in kiosk mode.
The welcome screen is written is plain javascipt and is available `here <https://github.com/FARI-brussels/Welcome-Screen>`_.

Totem
-----
The totem runs on a rasperry pi. The distribution is an arbian image similar to the one used for the other SBC and describe here 
:ref:`sbc`
However some additional steps are required to set up a distro for the totem:

1. In settings, display, set the orientation to portrait right
   
2. Use xinput to rotate the touch screen input
.. code-block:: bash
   sudo apt install xinput
   xinput list # to find the device id of the touch screen
   xinput set-prop "Touchscreen_Device_ID" --type=float "Coordinate Transformation Matrix" 0 -1 1 1 0 0 0 0 1



.. _scripts:
Scripts
-------

There is a collection of bash scripts in `this repository <https://github.com/FARI-brussels/TE-Scripts>`_
They are used to maintain an update the kernels installed on the different SBCs as well as to add a new demonstration.
Here is a description of the different scripts:

* **update_ips.sh**: Updates the IP addresses of SBCs in the CMS based on arp-scan results. This script is usefull because we currently don't have the possibility to have fixed local ips on BeCentral network.
* **enable_autologin.sh**: Enables autologin on SBCs to bypass the login screen. This script is used to avoid having to enter the passwords each time we start a SBC. It must be run once only.
* **create-desktop-icons.sh**: Generates desktop icons for each demonstration. This script is used to generate the desktop icons for each demo. It must be run once only.
* **clone_or_pull_repo.sh**: Utility script to clone or update a repository.
* **launch_welcome_screen.sh**: Starts the welcome screen.
* **update_all_devices.sh**: Updates all devices by running a command on them using SSH.
* **ssh_to_device.sh**: Provides SSH access to a specific SBC by its device name.
* **totem/totem.sh**: Launch the totem interface
More documentation about the scripts is available in the repository.
