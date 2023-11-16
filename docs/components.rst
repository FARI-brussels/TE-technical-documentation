Components
==========

.. _cms:

Content Management System
-------------------------

The experience center CMS is based on strapi. The documentation can be found [here](https://strapi.io/documentation/developer-docs/latest/getting-started/introduction.html).
It is currently hosted on Gandi and can be accessed [here](http://46.226.110.124:1337/admin/). If you need access to the CMS, please contact Siméon Michel.
We will soon migrate the CMS to a Strapi cloud infrastructure and the documentation will be updated accordingly.

The content management system contains the following collections:

1. **demo** (en/fr/nl)
   Contains all the information about the demos for the welcome screen to work properly. 
   The welcome screen of each demo call to the CMS to retrieve the information about the demo and display it on the screen.

2. **device**
   Contain all the information about the different devices (SBCs, smart plugs, etc.). This is useful for the :ref:`scripts` to work properly.
   It is mainly used to be able to retreive the local ip adress of the device if it has changed. If you add a new device you should register it there.

3. **Interface components** (en/fr/nl)
   Contains the multilingual content of the different interface components shared between different demos (buttons, titles, etc.)

4. **whichContentIsReal_MediaLists**
   This collection is used by the which content is real demo. It contains the different real/fake media pairs

5. **demo_chatbot** (en/fr/nl)
   his collection is used by the which content is real demo. It contains information about the different chatbot that can be used

.. _sbc:

Single Board Computers
----------------------

We currently have three different Single Board Computers (SBCs): Odroid C4, Odroid N2, and Raspberry Pi 4. 
All models run Armbian version 22 or greater with the GNOME desktop environment. 
Custom Fari images for each SBC can be found at the provided link (ADD LINK!).

⚠️ When you add a new SBC, please register its mac addres in the Content Management System (required for the scripts to work in case we don't have access to fixed local ips)

Setting Up a Fari image for a New SBC type
``````````````````````````````````````````

To prepare a new SBC with the Armbian image, follow these steps:

1. Download the latest Armbian image with GNOME desktop from here (https://www.armbian.com/download/?device_support=Supported.)
2. Use Balena Etcher or a similar tool to flash the image onto an SD card.
3. Insert the SD card into the SBC and power it on.
4. When prompted, set the root and user passwords to `fari.brussels` and choose `fari` as the username. Note: The default keyboard layout is QWERTY.
5. Select `bash` as the default shell.
6. During the initial setup, opt to skip Wi-Fi connection and locale generation (skip locales 154).

Initial System Update and Package Installation
``````````````````````````````````````````````

Run the following commands to update the system and install necessary packages:

.. code-block:: bash

   sudo apt update
   sudo apt upgrade
   sudo apt install python-is-python3 pip sshpass arp-scan jq dos2unix xdotool gnome-startup-applications

Repeat the update and upgrade commands to ensure all packages are up to date:

.. code-block:: bash

   sudo apt update
   sudo apt upgrade

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


.. autosummary::
   :toctree: generated


.. _sp:

Smart Plugs
-----------

All demos are wired to electricity through shelly smart plugs. The documentation can be found [here](https://shelly-api-docs.shelly.cloud/).
To access the dashboard, you can download the `shelly mobile app <https://play.google.com/store/apps/details?id=cloud.shelly.smartcontrol&hl=en_US>`_ or access to the `web app <https://control.shelly.cloud/>`_.
The credentials can be found on the test and experience password vault.

.. autosummary::
   :toctree: generated


.. _scripts:

Scripts
-------
