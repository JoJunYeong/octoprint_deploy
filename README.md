Updated May 2022.  
Want to support this work? Buy Me a Coffee. https://www.buymeacoffee.com/ppaukstelis.
Need help with octoprint_deploy? You can open issues here or ask on Discord: https://discord.gg/6vgSjgvR6u
# octoprint_deploy
These files provide a simple bash script for quickly deploying multiple octoprint instances on a single computer. For Linux systems (Ubuntu, Fedora, etc.) it will also install OctoPrint and a video streamer (mjpg-streamer or ustreamer).
# BIG CHANGES
As of 02/22 there is no longer a need to download a specific image file.

# How to use
* OctoPi
  * Slightly dated YouTube video for OctoPi setup here: https://www.youtube.com/watch?v=J5VzI4AFav4&lc
  * Put the latest OctoPi image on your SD card.
  * ssh into your Pi (pi@octopi.local; good idea to change your password now!).
  * run the command `git clone https://github.com/paukstelis/octoprint_deploy.git`.
  * run the command `sudo octoprint_deploy/octoprint_deploy.sh`.
  * Choose `Prepare System` from the menu.
  * If you have already been using this system for some time, you will be prompted that files will be moved in order to generate a template instance.
  * Setup admin user by connecting to http://octopi.local via browser.
  * Back in the ssh session, choose `Add Instance` and follow the instructions.
  * If your printer does not have a serial number (all Creality printers), it will time out and use the physical USB address for udev entries.
  * Continue until you have added all the printers you want to use.
  * haproxy entries are updated so you can connect via http://octopi.local/instancename/ (trailing slash is needed).
  * Please note, haproxy entries are NOT used for webcams once you use this system. Connect to them via hostname:port.
* General Linux (Ubuntu/Mint/RPiOS/Debian/Fedora/etc/)
  * __You do not need to install OctoPrint using any Wiki instructions, snap, etc. The script will do it for you.__
  * Basic guide video here: https://youtu.be/1YINWQ5fNn0
  * Install Ubuntu 18-22.X, Mint 20.3+, Debian, DietPi, RPiOS, Armbian, or Fedora35+ on your system (make sure your user is admin for sudo).
  * Install git if it isn't already: `sudo apt install git` or `sudo dnf install git`.
  * run the command `git clone https://github.com/paukstelis/octoprint_deploy.git`.
  * run the command `sudo octoprint_deploy/octoprint_deploy.sh`.
  * Choose `Prepare System` from the menu. Select your distribution type. All deb-based system use the same selection. This will install necessary packages, install OctoPrint, and start a template instance.
  * You will be asked if you want to use haproxy. This will make your instances available on port 80 (e.g. http://localhost/instancename).
  * You will be asked which streamer you would like to install (mjpg-streamer or ustreamer).
  * Setup admin user by connecting to your system (either http://localhost:5000 or http://[hostname]:5000 via a browser
  * __This instance is just a generic template used for making all your other instances. You need to make at least one instance using the script when this is done. Do not add a camera to the generic instance.__
  * Continue with octoprint_deploy script, choose `Add Instance` and follow the instructions.
  * If your printer does not have a serial number (all Creality printers) allow the auto-detection to time-out and it will detect by the USB port you plugged it in to.
  * Add as many instances as you have printers, following the instructions.
  * Remember, camera installed with this script are experimental and always will be. The script makes some basic assumptions that you may need to change later. Cameras suck up quite a bit of USB bandwidth so while it is quite straightforward to run 10 printers with a modest computer, you can't also run 10 cameras.
* What else can you do?
  * Remove instances
  * Add USB webcams AFTER you've created the instance
  * Test USB connections
  * Want to get rid of everything? `sudo octoprint_deploy/octoprint_deploy.sh remove`
# Recent Changes
* Prompt for haproxy for linux installs
* Implement 'Use all defaults' for adding instances.
* Prompt for streamer (mjpeg-streamer or ustreamer)
* Uniquify pnp uuid.
* Add duplicate serial number detection.
* Add architecture check to minimize errors where a system gets prepared as OctoPi when someone is using Ubuntu/Fedora/etc.
* Include ustreamer as an option for camera streaming
* Add remove command-line argument to get rid of all the stuff the script has done.
# TODO
* Uniquify tracking ids
* Cameras behind haproxy?
* Add Arch (pacman) support

