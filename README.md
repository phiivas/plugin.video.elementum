![](http://i.imgur.com/4eQhijh.png)

[![Build Status](https://travis-ci.org/scakemyer/plugin.video.quasar.svg?branch=master)](https://travis-ci.org/scakemyer/plugin.video.quasar)

What it is
----------
Quasar is an torrent finding and streaming engine. It doesn't go on torrent websites for legal reasons. However, it calls specially crafted addons (called providers) that are installed separately. They are normal XBMC addons, and thus can be installed/updated/distributed just like any other addon.

This project is a fork of the well known, but no longer maintained Pulsar project from [steeve](https://github.com/steeve/plugin.video.pulsar).
Big thanks for his great job.

Supported platforms
-------------------
- Windows
- Linux 32/64 bits (starting Ubuntu 12.04)
- Linux ARM (Raspberry Pi, Cubox i4pro etc...)
- OS X 64 bits
- Android ARM (4.x)

Build
-----
If you want to build this plugin, feel free. First, build the quasar daemon (see the [quasar project](https://github.com/scakemyer/quasar) for more information). Then, create a symlink, like this:
```
ln -s $GOPATH/src/github.com/scakemyer/quasar/build ./resources/bin
```
and build the package:
```
make
```

Download
--------
See the [Releases](https://github.com/scakemyer/plugin.video.quasar/releases) page.


Installation
------------
- Install Quasar like any other addon
- Go in Settings > Services > Remote Control and **enable both options**
- Restart XBMC


How it works
------------
Quasar is a torrent finding and streaming engine. **It doesn't go on torrent websites for legal reasons**. It calls specially crafted addons (called **providers**) that are installed separately. They are normal XBMC addons, and thus can be installed/updated/distributed just like any other addon.

Quasar is centred around media: it browses media from [TheMovieDB](https://www.themoviedb.org/) and [TheTVDB](http://thetvdb.com/).
And so, when you decide you want to watch a media (i.e. given an IMDB or TVDB Id), here's what Quasar does:

- Enumerate the installed providers
- Call each provider to find the media you want to watch (in parallel)
- Each provider returns a list of BT links they found
- Collects and de-duplicates all the links
- Goes on the BitTorrent network to find out the number of seeds and peers in real time (i.e. not provided by the provider)
- Finds out of which quality are the different links (thanks to their name)
- Ranks the links by quality and availability (Quasar privileges quality over availability, but it's not dumb. However, you can get a full list to choose from manually it you want, or enable 'Choose Stream by default' to always choose manually)
- Sends the chosen link to the BitTorrent streaming engine (brand new, and completely rewritten)

All of this is done in less than 1s. Quasar is around 95% Go, and thus, it's *fast*. Very fast, actually.

The BitTorrent streaming engine is brand new and very resilient (or at least it's designed to be). It's built on top of the brand new libtorrent 1.0 (which had special patches for the streaming case). So it's very optimised, especially for low CPU machines. I have yet to find a media that doesn't play with the engine.


Providers
---------
As said before, Quasar **relies on providers to find streams**. Providers are easy to write, and average ~20 lines of Python. As they are normal XBMC addons, which can have their own configuration (although it is not recommended because it complicates things).

Sample Quasar provider: [https://github.com/steeve/script.quasar.dummy](https://github.com/steeve/script.quasar.dummy)

Providers are given a max amount of time to run before Quasar considers them to be too slow. The timeouts are as follow:
- 4 seconds on Intel CPUs
- 20 seconds on multicore ARM CPUs
- 30 seconds on single core ARM CPUs (Raspberry Pi)

Please note that for legal reasons, **I won't discuss, develop nor distribute any providers connecting to illegal sources**. So there is no need to ask me.
While I can partake in general discussions regarding provider development, **I won't do so for illegal sources specific problems**.


FAQ
---
##### I can't code. How can I help?
Spread the word. Talk about it with your friends, show them, make videos, tutorials. Talk about it on social networks, blogs etc...

##### The plugin doesn't work, what can I do?
Put your xbmc.log on [pastebin](http://pastebin.com/).
If you don't know how to do that, just follow the guide at: [http://kodi.wiki/view/Log_file/Easy](http://kodi.wiki/view/Log_file/Easy)

##### Can I seek in a video?
Yes, but it can fail.

##### What about seeding?
When watching a torrent, **you will be seeding while you watch the stream**.

##### Does it downloads the whole file? Do I need the space? Is it ever deleted?
Yes, yes and yes.

##### Can I keep the file after watching it?
Yes, change it in the addon settings.

##### Can I set it to download directly to my NAS?
Yes, but **you need to mount your NAS via the OS, not via XBMC**.

##### Provider X is blocked in my country/ISP, how can I set another domain?
Sorry, I won't comment of specific providers.

##### Will there be an Android version?
Yes. I have a working version right now, but it's not stable enough for release. Don't blame me, the Android ecosystem is pretty bad for that sort of thing.


Screenshots
-----------
![](http://i.imgur.com/uchej1p.png)
![](http://i.imgur.com/0ybvekN.jpg)
![](http://i.imgur.com/L103Xt1.jpg)
![](http://i.imgur.com/8qSwVk1.jpg)
