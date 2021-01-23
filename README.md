# DEEPi OS #

## Quick Start ##

Flash a new RPi OS microSD card and place the contents of `boot/` into the
the `/boot` directory then boot. Edit `wpa_supplicant.conf` as necessary.

<!-- TODO: include usb-over-ethernet instructions -->

Using `sudo raspi-config` change the following settings.

  * [ ] Enable camera
  * [ ] Expand GPU memory to 256MB
  
Download or clone this repo on the new RPi.

```
sudo sh ./setup.sh
```

Open a browser to http://deepi.local/

## Camera Control ##

The camera is run by the UV4L driver. The driver creates a device at
`/dev/video0` which can be accessed by different software. 

The camera can also be controlled using the python `picamera` library
or using the included `raspistill` and `raspivid` commands. The camera
can only be accessed by one software at a time. 

## Live Feed ##

The live feed is handled the UV4L-WebRTC. It can be viewed and
controlled through a browser on port 8080.

## Camera Commands ##

Camera commands are located in `/usr/local/bin/`.

  * [ ] more commands
  * [ ] add error checking
  * [ ] status command

Commands can be scheduled using the crontab interface using the command
`crontab -e` or `sudo crontab -e`. 
  
### Snapshot ###

The command `snapshot` gets the latest frame from the camera and saves
it with a timestamp to `/home/pi/pictures/`. Settings are controlled
by `/etc/uv4l/uv4l-raspicam.conf` and match the settings from the live
feed.

## Interfaces ##


### SSH ###

SSH is enabled on the DEEPi by default. SSH gives the user complete
command line control including passwordless sudo privileges.

### FTP ###

The DEEPi runs a [proftpd]() FTP server. This allows quick transfer of
files on and off the device. Files can be accessed using FTP clients
such as Filezilla.

  * [ ] Consider swtiching to
        [pureftp](https://www.raspberrypi.org/documentation/remote-access/ftp.md)

### HTTP ###

The DEEPi runs a [lighttpd]() HTTP server. This allows users on the same
network to interact with the DEEPi through the browsers. The index page 
contains useful instructions.

Web server files are located at `/var/www/html/`. 

  * [ ] Expand webserver information and manual

#### CGI-BIN ####

CGI-BIN commands can be run through the web interface. The binaries are 
located in `/usr/lib/cgi-bin/` and can be run by sending HTTP requests to
`/cgi-bin/`.

  * [ ] more commands

### Time Sync ###

DEEPi uses `timedatectl` to synchronize with ntp servers. The configuration
file is located at `/etc/systemd/timesyncd.conf`.

  * [ ] Get time sync working. The university network may be the problem, 
		but I cannot tell.
