# selfie-app
#

**To setup a brand new Raspberry Pi from scratch.**

Prerequisites.

- libcups2-dev
- libcupsimage2-dev
- g++
- cups
- cups-client
- lpr
- inotify-tools
- any printer.

** Before I get to writing a lovely script to install and set all this up automatically, just do the following. **

__ FROM ANYWHERE __

sudo apt-get update
sudo apt-get upgrade
sudo apt-get install libcups2-dev libcupsimage2-dev g++ cups cups-client lpr inotify-tools

Inside zj-58 Folder...

sudo ./install

From setup folder.

copy App.py to /usr/local/lib/python2.7/instagram-scraper to replace the existing app.py file.

copy selfie-app_instagram_print to /etc/systemd/system
run sudo systemctl daemon-reload
 
copy selfie-app_batch_print to /etc/systemd/system
run sudo systemctl daemon-reload

./run_instagram_scraper to start the scraper manually.
./run_batch_print to start the printer manually.

sudo systemctl start selfie-app_instagram_print to start the selfie-app instagram scraper service.
sudo systemctl start selfie-app_batch_print to start the selfie-app batch printer service.





