# Installation:

`sudo eopkg it gestures`

### Setup:

Add your user to the input group.

`sudo usermod -a -G input YOUR_USERNAME`
Note: You will have to log out and back in before continuing.

### Start the libinput daemon

`libinput-gestures-setup start`
If all goes well then you should set the daemon to autostart at boot

`libinput-gestures-setup autostart`

### Configuration:

My personal configuration is setup to switch between work spaces with three fingers. Similar to MacOS.
