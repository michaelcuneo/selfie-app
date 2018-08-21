### Selfie-App - Written as a supplement to automate the processes of duplicating the services of Instagram Scraping and Printing for Ralph Kenke & Elmar Trefz Selfie Factory Installation ###

## NB. Clone this repository to ~/home/pi/Desktop/ I'll write something better to run the service from elsewhere later. ##

**TODO:**
- [ ] Write an automated script to set everything up properly.
- [ ] Write a script to automate the CRON setup.

**To setup a brand new Raspberry Pi from scratch.**

Prerequisites.

- libcups2-dev
- libcupsimage2-dev
- g++
- cups
- cups-client
- cups-bsd
- inotify-tools
- https://github.com/adafruit/zj-58 or any other printer.
- https://github.com/rarcega/instagram-scraper

**Before I get to writing a lovely script to automatically install everything from scratch... just do the following, to set up the service on any rPI's**

__FROM ANY FOLDER__

Update the local apt repositories.
```console
pi@raspberrypi:~$ sudo apt-get update
```
Upgrade to the latest version of everything.
```console
pi@raspberrypi:~$ sudo apt-get upgrade
```
Grab the prerequisites.
```console
pi@raspberrypi:~$ sudo apt-get install libcups2-dev libcupsimage2-dev g++ cups cups-bsd cups-client inotify-tools
```
Add the user pi, to the lpadmin group so you can run CUPS Administration.
```console
pi@raspberrypi:~$ sudo usermod -a -G lpadmin pi
```
Install adafruit zj-58 driver from https://github.com/adafruit/zj-58
 or other printer driver.
 
Add the printer inside CUPS Administration.
* Goto http://localhost:631/admin and add your printer.
* If the printer is a ZJ-58 use the following settings to prevent it spitting out crap in between images.
  * BAUD RATE = 2400 (Yes it will show up as connected at 115200, ignore it)
  * Bits = 8
  * Parity = NONE
  * Flow Control = NONE

Install Instagram Scraper from https://github.com/rarcega/instagram-scraper
```console
pi@raspberrypi:~$ sudo pip install instagram-scraper
```

__From setup folder__

There's an issue with the latest instagram-scraper python app. Replace the app.py with the app.py included.
* copy App.py to /usr/local/lib/python2.7/instagram-scraper to replace the existing app.py file.
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp app.py /usr/local/lib/python2.7/instagram-scraper
```

* copy selfie-app_instagram-scraper.service to /etc/systemd/system
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp selfie-app_instagram-scraper.service /etc/systemd/system
```
* copy selfie-app_batch-print.service to /etc/systemd/system
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp selfie-app_batch-print.service /etc/systemd/system
```
* Restart the systemctl daemon
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo systemctl daemon-reload
```

### AND NOW YOU'RE GOOD TO GO! ###

#### to start the scraper manually. ####
```console
pi@raspberrypi:~/Desktop/selfie-app $ ./run_instagram_scraper
```
#### to start the printer manually. ####
```console
pi@raspberrypi:~/Desktop/selfie-app $ ./run_batch_print
```
#### to start the selfie-app instagram scraper service. ####
```console
$ sudo systemctl start selfie-app_instagram-scraper.service
```
#### to start the selfie-app batch printer service. ####
```console
$ sudo systemctl start selfie-app_batch-print.service
```
