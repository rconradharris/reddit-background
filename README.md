reddit-background
=================

Set your Mac OS X or Linux desktop background to images pulled from [Reddit](https://reddit.com)

![Screenshot](https://raw.githubusercontent.com/rconradharris/reddit-background/master/screenshot.jpg)

Features
--------

- Supports multiple monitors (Mac OS X only)
- Handles multiple subreddits
- Aspect ratio and resolution filtering ensures your backgrounds are always beautiful
- Flexible sorting lets you choose the quality of images it downloads
- Optionally imprints the title on each image
- Can pick images that match the current season
- Download only option (`--image-count`) if you want to use OS X's existing
  folder-based background selector

Try It
------

1.  Download the project; or clone the repo using [git](http://git-scm.com/),
    like:

        git clone https://github.com/rconradharris/reddit-backgrounds.git

2.  Run it:

        cd reddit-background
        ./reddit-background

The default is to use images based on the current season (`{seasonal}`), so
for example, if it’s November, the images will be pulled from
    [/r/AutumnPorn](https://reddit.com/r/AutumnPorn).

Install It
----------

The easiest way to install reddit-background is to copy it to
`/usr/local/bin`. To do this, run this command:

    cp reddit-background /usr/local/bin

Configure It
------------

If you'd like to customize reddit-background so that it chooses images images
from different subreddits, you can provide a configuration file at
`~/.reddit-background.conf`. Samples configuration files are provided in the
[examples](https://github.com/rconradharris/reddit-background/tree/master/examples)
directory.

Automate It
-----------

Once you have a configuration you like, you can set up reddit-background to
rotate your background daily.

There are a number of ways to do this, but one way is to add it to your *crontab*.

To do this, open up your crontab in an editor:

    crontab -e

And once you’ve done that, add the following line:

    0 9 * * * /usr/local/bin/reddit-background

Save the file and quit the editor. Now your background will rotate daily at
9:00 in the morning.

Advanced
--------

### Subreddit Sort Options

By default, when you specify a subreddit, you are selecting the top 25 posts
over the last month.

You can customize the sort by using the following format:

    <subreddit>:[sort]:[limit]:[timeframe]

| Argument  | Possible Values                                        | Default |
|-----------|--------------------------------------------------------|---------|
| subreddit | A subreddit or {seasonal}                              | *None*  |
| sort      | contraversial, gilded, hot, new, promoted, rising, top | top     |
| limit     | An integer                                             | 25      |
| timeframe | all, day, hour, month, week, year                      | month   |

So, for example, if you want to only include the 5 newest posts from
[/r/EarthPorn](https://reddit.com/r/EarthPorn), you would write it as:

    EarthPorn:new:5

Or if you’d like to include the top 10 posts over the year for
[/r/CityPorn](https://reddit.com/r/CityPorn), you’d write it as:

    CityPorn:top:10:year

**NOTE:** Only the `top` and `controversial` sort methods use the `timeframe` option.

### Dynamic Subreddits

reddit-background can dynamically pull images from the correct subreddit based
on some criteria.

These are called 'dynamic subreddits' and they are specified just like normal
except they are enclosed in curly-brackets.

Currently the only one included is `{seasonal}` which will choose from amongst
[/r/WinterPorn](https://reddit.com/r/WinterPorn),
[/r/SpringPorn](https://reddit.com/r/SpringPorn),
[/r/SummerPorn](https://reddit.com/r/SummerPorn), or
[/r/AutumnPorn](https://reddit.com/r/AutumnPorn) based on the current season
(in the northern hemisphere).


### Command-Line Usage

In addition to specifying a configuration file, you can also customize
reddit-background directly from the command-line.

The arguments represent each subreddit you would like to pull images from. For
example, to pull seasonal images and images from
[/r/CarPorn](https://reddit.com/r/CarPorn), you would run:

    reddit-background {seasonal} CarPorn

If you have a multi-monitor setup, you can also set the background for a
single monitor using the `--desktop` option like:

    reddit-background --desktop 1 BeachPorn

This will set the background on desktop 1 to one of the 5 hottest posts from
[/r/BeachPorn](https://reddit.com/r/BeachPorn).

### Download Configuration

By default reddit-background will download a single image per desktop and set
that to your desktop's background.

In addition, you can use OS X's native folder-based background selector which
offers additional features.

To use OS X's background selector, you tell `reddit-background` to download a
set number of images using the `--image-count` option. This will download these
images into the download directory but not actually set them as the
background. You then set `System Preferences -> Desktop -> Backgrounds` to
point to the download directory for each desktop.


### Scale to Desktop Size

By default, images are downloaded in their original resolution.  When the "fit" option is set, reddit-background fits the image to your screen
resolution by adding black bars where needed.  

While your OS likely has this option already, using this configuration option makes sense when
paired with the "Imprint Title" option.  By scaling the image first and then imprinting the title, 
you get a consistent font size as well as a guarantee the imprint will be on the screen (and not 
scaled off one side or the other).

This option can be set as a default for all desktops or can be set individually per desktop.  The following
configuration enables fitting for all downloaded images:

    [default]
    fit_images = True
    
    
### Show Title of Image

If you'd like to know the title of the background you're looking at, you have
three different options.

First, on the command-line you can run:

    reddit-background --what
    Desktop 1
        Perth, Western Australia, from Elizabeth Quay [5376x3024].jpg

Second, you can enable the `desktop_symlinks=True` configuration. This
will place a symlink on you desktop to your current images. This gives you
easy access to the image, but more importantly, shows you the title of the
image.

Third, you can imprint the title directly on the image itself.  This option
requires that you load additional modules into Python.  This option works
best when paired with `fit_images=True`.

#### Prerequisites for Imprinting Titles

Imprinting requires the Python Imaging Library.  We suggest installing the 
[Pillow](https://python-pillow.org/) fork of this library.  The directions below
are a quick guide.  Full documentation is available on the pillow site.

Windows users can download an installable binary from the pillow site.

Mac and Linux users should ensure they have `freetype` and `libjpeg` installed
**before** installing `pillow`.  Linux likely has these already, and Mac
users can add them with:

    brew install freetype libjpeg
    
Once you have these dependencies are available on your system, install
pillow with one of the following commands:

    pip install Pillow
    # or
    easy_install Pillow

#### Imprinting Configuration

Configuration can be done globally in the `[default]` section or per desktop.
If you specify desktop sections, the default section is entirely ignored.
The options are as follows:

    imprint_position=<horizontal> <vertical>
    imprint_size=[box width]:[margin]:[padding]:[transparency]
    imprint_font=[font filename]:[font size]:[font color]

The first option, `imprint_position`, is required and is what activates 
imprinting.  The others are optional.

| Argument      | Possible Values                                          | Default |
|---------------|----------------------------------------------------------|---------|
| horizontal    | top, center, bottom                                      | center  |
| vertical      | left, center, right                                      | center  |
| box width     | number of pixels before line wrap                        | 500     |
| margin        | number of pixels from the edge of image                  | 50      |
| padding       | number of pixels inside of text box                      | 8       |
| transparency  | number from 0 to 100 for percent transparency (text box) | 40      |
| font filename | filename of TrueType font on your system to use          | Arial   |
| font size     | font size                                                | 50      |
| font color    | hex code: #112233, or RGB triple: (255, 128, 75)         | #E8BC61 |

Example 1: the following configuration places the title at the bottom-left corner of the image. It
uses the defaults for font and size:

    [default]
    fit_images=True
    imprint_position=bottom left

Example 2: the following configuration centers the title 200 pixels from the top of the image.  It won't
wrap lines because the box width is set so large.  The zero transparency makes the box background
invisible. A custom font, size, and color are set.

    [default]
    fit_images=True
    imprint_position=top center
    imprint_size=2000:200:10:0
    imprint_font=Perpetual Bold:20:#3CB371

Since the program cannot know how your OS will scale the image, placement 
is relative to the image itself and not to your desktop.
In other words, a placement of "top left" means the top-left corner of the **image**.  
If your desktop cuts off the top of your image (in order to cover the entire desktop), 
the title box will not be visible.  The solution is to always 
set `fit_images=True` to ensure images are fit to your desktop size before imprinting is
done.

Note that font filenames are not always the same as the displayed name in OS dialog boxes.
For example, the filename for "American Typewriter" on my machine is "AmericanTypewriter.ttf"
(without a space).  The extension can be omitted, and only TrueType fonts are supported.

Transparency affects the text box background only (not the title text). This semi-transparent
box is added behind the title because no color is appropriate across all images.  If you 
use a white font, some images will have white pixels in the title area.  If you instead use
a black font, other images will have black pixels in the same area.  The box allows 
your desired color to be read regardless of the image colors beneath the title.

#### Imprinting with Command-Line Options

Options can be specified on the command line, as in the following example:

    reddit-background --imprint-position="top right" --imprint-size=1000:500:100:70 --imprint-font="Arial:50:#888888"

### Image Choosing Algorithms

There are two algorithms included to pick images for you. The first one is
called 'random', and will select images randomly. This is good if you want the
most possible variety.

The other algorithm--the default--is called 'bestmatch' and will use Reddit score, aspect
ratio, resolution, and tiny bit of randomness to select images that will look
good on your particular desktop.

You can select which algorithm to use in the configuration file like so:

    image_chooser=random
