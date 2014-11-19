=================
reddit-background
=================

Sets your Mac OS X desktop background to images pulled from Reddit.


Features
========

* Handles multiple desktops (each desktop gets its own image)
* Handles multiple subreddits (subscribe to r/EarthPorn, r/Wallpapers, etc...)
* Seasonal awareness (if it's spring, automatically include images from
  r/SpringPorn)


Installation
============

1. Clone the repo::

   git clone https://github.com/rconradharris/reddit-backgrounds.git

2. Copy exectuable to ``/usr/local/bin``::

    cd reddit-background
    cp reddit-background /usr/local/bin

3. Open your crontab::

   crontab -e

4. And paste one of the following lines

   For hourly::

        0 * * * * /usr/local/bin/reddit-background --seasonal wallpaper

   For daily at 09:00::

        0 9 * * * /usr/local/bin/reddit-background --seasonal wallpaper


5. Edit the subreddits in the line to match your preferences

6. Save and quit the editor

7. Enjoy!


Manual Usage
============

You can also change backgrounds on demand by running the command manually.


Just (northern hemisphere) seasonal images::

    ./reddit-background --seasonal


Seasonal images plus images pulled from r/earthporn and carporn::

    ./reddit-background --seasonal EarthPorn CarPorn


Pull images just from r/wallpaper::

    ./reddit-background wallpaper


Set desktop 1 to r/CarPorn and desktop 2 to r/EarthPorn::

    ./reddit-background --desktop 1 CarPorn
    ./reddit-background --desktop 2 EarthPorn


Author
======

Rick Harris <rconradharris@gmail.com>
@rconradharris
