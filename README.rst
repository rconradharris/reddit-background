=================
reddit-background
=================

Sets your Mac OS X desktop background to images pulled from Reddit.


Features
========

* Supports multiple desktops (each desktop gets its own image)
* Handles multiple subreddits (subscribe to r/EarthPorn, r/Wallpapers, etc...)
* Powerful sorting (optionally specify sort method, timeframe and limit for
  each subreddit)
* Dynamic subreddits (for example ``{seasonal}`` will automatically choose the
  correct subreddit based on the current month)


Installation
============

1. Clone the repo::

   git clone https://github.com/rconradharris/reddit-backgrounds.git

2. Copy exectuable to ``/usr/local/bin``::

    cd reddit-background
    cp reddit-background /usr/local/bin

3. Create a config file located at ``~/.reddit-background.conf`` and edit to
   your liking (You can skip this step and it will default to seasonal images)::

    # Use across all desktops
    [default]
    subreddits={seasonal}

    # Override to use these subreddits on desktop 1
    #[desktop1]
    #subreddits=EarthPorn

    # Override to use these subreddits on desktop 2
    #[desktop2]
    #subreddits=CarPorn

4. Open your crontab::

   crontab -e

5. And paste one of the following lines

   For hourly::

        0 * * * * /usr/local/bin/reddit-background

   For daily at 09:00::

        0 9 * * * /usr/local/bin/reddit-background


6. Save and quit the editor

7. Enjoy!


Subreddit Format
================


Subreddits are described using the following format::

    <subreddit>:[sort]:[limit]:[timeframe]

``sort`` defaults to 'top'. Available: 'hot', 'new', 'rising', 'controversial', 'top', 'gilded' and 'promoted'
``limit`` defaults to 25
``timeframe`` defaults to 'week'. Available: 'hour', 'day', 'week', 'month', 'year', 'all'

So, if you want to include images from CarPorn using a the top 10 posts over
the year, you would use::

    CarPorn:top:10:year

If you only want the 5 newest EarthPorn images, you would use::

    EarthPorn:new:5

Only the 'top' and 'controversial' sort methods use the ``timeframe`` option.


Dynamic Subreddits
==================

Dynamic subreddits are automatically chosen according to some criteria. For
example the ``{seasonal}`` subreddit will rotate with the seasons: in the spring
it maps to r/SpringPorn, in winter to r/WinterPorn, etc.

Right now, ``{seasonal}`` is the only dynamic subreddit available.

You can use dynamic subreddits with additional options like::

    {seasonal}:top:10:day


Config File
===========

reddit-background will look for a config file located at ``~/.reddit-background.conf``.

The format is::

    # Use across all desktops
    [default]
    subreddits={seasonal},CarPorn:new

    # Override to use these subreddits on desktop 1
    [desktop1]
    subreddits=EarthPorn

    # Override to use these subreddits on desktop 2
    [desktop2]
    subreddits=BeachPorn


Manual Usage
============

You can also change backgrounds on demand by running the command manually.


Just (northern hemisphere) seasonal images::

    ./reddit-background {seasonal}


Seasonal images plus images pulled from r/EarthPorn and CarPorn::

    ./reddit-background {seasonal} EarthPorn CarPorn


Pull images just from r/wallpaper with the top 10 posts over the year::

    ./reddit-background wallpaper:top:10:year


Set desktop 1 to the 5 hottest posts from r/CarPorn and desktop 2 to new posts from r/EarthPorn::

    ./reddit-background --desktop 1 CarPorn:hot:5
    ./reddit-background --desktop 2 EarthPorn:new


Author
======

Rick Harris <rconradharris@gmail.com>
Twitter: @rconradharris
