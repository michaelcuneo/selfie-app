### Selfie-App - Written as a supplement to automate the processes of duplicating the services of Instagram Scraping and Printing for Ralph Kenke & Elmar Trefz Selfie Factory Installation ###

**TODO:**
- [ ] Write an automated script to set up everything.
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

**Before I get to writing a lovely script to automatically install everything from scratch... just do the following, to set up the service on additional rPI's**

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
pi@raspberrypi:~$ sudo apt-get install libcups2-dev libcupsimage2-dev g++ cups cups-client lpr inotify-tools
```
Add the user pi, to the lpadmin group so you can run CUPS Administration.
```console
pi@raspberrypi:~$ sudo usermod -a -G lpadmin pi
```
Install adafruit zj-58 driver from https://github.com/adafruit/zj-58
 or other printer driver.
 
Add the printer inside CUPS Administration.
* Goto http://localhost:631/admin and add your printer.

Install Instagram Scraper from https://github.com/rarcega/instagram-scraper
* pip install instagram-scraper

__From setup folder__

There's an issue with the latest instagram-scraper python app. Replace the app.py with the app.py included.
* copy App.py to /usr/local/lib/python2.7/instagram-scraper to replace the existing app.py file.
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp app.py /usr/local/lib/python2.7/instagram-scraper
```

* copy selfie-app_instagram_print to /etc/systemd/system
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp selfie-app_instagram_print to /etc/systemd/system
```
* copy selfie-app_batch_print to /etc/systemd/system
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo cp selfie-app_batch_print to /etc/systemd/system
```
* Restart the systemctl daemon
```console
pi@raspberrypi:~/Desktop/selfie-app/setup $ sudo systemctl daemon-reload
```

**AND NOW YOU'RE GOOD TO GO!**

#### to start the scraper manually. ####
* ./run_instagram_scraper
#### to start the printer manually. ####
* ./run_batch_print 
#### to start the selfie-app instagram scraper service. ####
* sudo systemctl start selfie-app_instagram_print
#### to start the selfie-app batch printer service. ####
* sudo systemctl start selfie-app_batch_print 
