# dynamic_wallpaper

A shell script to rotate through wallpaper sets throughout the day a'la MacOS

## Why

TBD: Justification, features, etc

## Installation

First, read the code and make sure that you're satisfied that it's safe.

I am not going to ever suggest that you do something like `curl` it to your system.

You may download it to your system in whatever way you feel comfortable.

You may install it on your system wherever you feel comfortable.

For me, I have it in `"${HOME}/bin`.  You might like it in `/usr/local/bin`, or
anywhere else that you prefer.

Create a cronjob for it using something like `crontab -e` or whatever works best
for you.  You might like to have it run every 10 minutes or so, so you might have
a cron entry that looks like

```bash
10 * * * * /home/rawiri/bin/dynamic_wallpaper awesome_image_set
```

## Where to get dynamic wallpapers

To be absolutely clear: I do not know the copyright status of any of these sources.
That is why I have not collated them into this repo.  Download at your own legal risk etc.

Some will need adjustment in order to work with this script.

Some may need you to hand-craft the config files to get the exact behaviour you want.

* https://dynamicwallpaper.club/
* https://github.com/karmanyaahm/awesome-plasma5-dynamic-wallpapers
* https://github.com/GitGangGuy/dynamic-wallpaper-improved/tree/master/images

## Configuration format

The config file is broadly based around the following format:

```bash
start:finish:filename
```

Where **start** and **finish** are in seconds relative to midnight.

For an image set containing only 2 images, we might have image1 as the daytime
and image2 as the nighttime picture.  The config would look something like:

```bash
0:27660:image2.jpeg
27660:61980:image1.jpeg
61980:86400:image2.jpeg
```

So between midnight (0 seconds) and sunrise (0741hrs -> 27660 seconds), we have our
night time image.  Between sunrise and sundown (1713hrs -> 61980 seconds), we have
our day time image.  Between sundown and midnight, we have our night time image.

FYI: The above example times were the correct times for my location in mid July 2021.

If you want to loop over a sequence of images within a time block, you can use:

```bash
start:finish:loop:<duration>:seq,<duration>:uence,<duration>:of,<duration>:images
```

For example:

```bash
27660:61980:loop:5:image3.jpeg,5:image4.jpeg,10:image5.jpeg
```

Would rotate around image3.jpeg for 5 seconds, image4.jpeg for 5 seconds and image5.jpeg for 10 seconds.

If there's more than one image in the set, we work on the following logic:

* Between sunset and sunrise, we use the last image in the set
* We sequence the rest in reverse order and then in-order
  * i.e. sunrise -> sunpeak -> sunpeak -> sunset.

For example, with an 8 image set:

* Overnight: 8
* Daytime: 7, 6, 5, 4, 3, 2, 1, 2, 3, 4, 5, 6, 7

```bash
#Example of the above config to be done here
```

## Alternative solutions

* https://github.com/saint-13/Linux_Dynamic_Wallpapers
* https://github.com/zzag/plasma5-wallpapers-dynamic
* https://github.com/GitGangGuy/dynamic-wallpaper-improved
