=================
reddit-background
=================

Sets your Mac OS X desktop background to images pulled from Reddit.


Features
========

* Supports multiple monitors
* Allows you to pull images from multiple subreddits
* Can pull images that match the current season
* Powerful sorting lets you choose the quality of images it downloads
* Filtering based on image resolution ensures your desktop backgrounds are
  always beautfully rendered


Try It
======

1. Clone the repo::
    
    git clone https://github.com/rconradharris/reddit-backgrounds.git

2. Run it::

    cd reddit-background
    ./reddit-background

The default is to use images based on the current season (``{seasonal}``), so
for example, if it's November, the images will be pulled from *r/AutumnPorn*.


Install It
==========

The easiest way to install reddit-background is to copy it to
``/usr/local/bin``. To do this run this command::

    cp reddit-background /usr/local/bin


Configure It
============

reddit-background lets you specify a configuration file so that you can
customize which subreddits it pull images from.

To use a custom configuration, create a file at ``~/.reddit-background.conf``.
Here's a sample to get you started::

    # Default is used across all monitors, unless overriden with a more
    # specific configuration
    [default]

    # {seasonal} will choose the correct subreddit based on the current season
    subreddits={seasonal}

    # Filter out any images with resolution below this
    min_resolution=1280x1024

    # Desktop 2 overrides the defaults to use images pulled from r/CarPorn and
    # r/EarthPorn
    [desktop2]
    subreddits=CarPorn,EarthPorn


Automate It
===========

Once you have a configuration you like, you can set up reddit-background to
rotate your background daily.

There are a number of ways to do this, but one way is to add it to your
*crontab*.

To do this, open up your crontab in an editor::

   crontab -e

And once you've done that, add the following line::

    0 9 * * * /usr/local/bin/reddit-background

Save the file and quit the editor. Now your background will rotate daily at
9:00 in the morning.


Advanced
========

Subreddit Sort Options
----------------------


By default, when you specify a subreddit, you are selecting the top 25 posts
over the last week.

You can customize the sort by using the following format::

    <subreddit>:[sort]:[limit]:[timeframe]

========= ====================================================== =======
Argument  Possible Values                                        Default
========= ====================================================== =======
subreddit A subreddit or {seasonal}                              *None*
sort      contraversial, gilded, hot, new, promoted, rising, top top
limit     An integer                                             25
timeframe all, day, hour, month, week, year                      week
========= ====================================================== =======


So, for example, if you want to only include the 5 newest posts from
*r/EarthPorn*, you would write it as::

    EarthPorn:new:5


Or if you'd like to include the top 10 posts over the year for CarPorn, you'd
write it as::

    CarPorn:top:10:year


**NOTE:** Only the 'top' and 'controversial' sort methods use the ``timeframe`` option.


Dynamic Subreddits
------------------

reddit-background can dynamically pull images from the correct subreddit based
on some criteria.

They are specified just like normal subreddits except they are enclosed in
curly-brackets.

Currently the only one included is ``{seasonal}`` which will choose from
amongst *r/WinterPorn*, *r/SpringPorn*, *r/SummerPorn*, or *r/AutumnPorn*
based on the current season (in the northern hemisphere).


Command-Line Usage
------------------

In addition to specifying a configuration file, you can also customize
reddit-background directly from the command-line.

The arguments represent each subreddit you would like to pull images from. For
example, to pull seasonal images and images from *r/CarPorn*, you would run::

    reddit-background {seasonal} CarPorn


If you have a multi-monitor setup, you can also set the background for a
single monitor using the ``--desktop`` option like::

    reddit-background --desktop 1 CarPorn:hot:5

This will set the background on desktop 1 to one of the 5 hottest posts from
*r/CarPorn*.

If you already know the URL of the image you'd like to use, you can use the
``--url`` to automatically download it and set it the background. For
example::

    reddit-background --url http://www.visit2ethiopia.com/images/Addis%20Ababa01.jpg

Author
======

* Rick Harris <rconradharris@gmail.com>
* Twitter: `@rconradharris<https://twitter.com/rconradharris>`_
