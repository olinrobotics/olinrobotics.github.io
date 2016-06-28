# Cross Project Info
This page is a collection of documentation for aspects of different robo lab projects which may be useful for multiple different projects.  It should contain short descriptions of the work you did with links to full documentation of what you did.

## Odroid Setup
Odroids are computers on a chip which we would like to mount on air vehicles to run code on boad the vehicle, rather than sending information down to a ground computer and sending control signals back up.

There were a couple of places we had to go to setup the Odroid:
- We used the most recent image [from here](http://east.us.odroid.in/ubuntu_14.04lts/) and have tested both the minimal and lubuntu images.
- We followed [these instructions](http://odroid.us/mediawiki/index.php?title=Step-by-step_Ubuntu_SD_Card_Setup) to flash the SD card with the image.
- After following these instructions, we had to edit the `boot.ini` file to set the resolution of the connected display before we could see the image (instructions for editing the file are in comments in the file)


