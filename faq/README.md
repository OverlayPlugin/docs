# FFXIV ACT FAQ
<!--
## Current stuff

The following information is accurate as of 2020-12-08 / patch 5.4:

* **Is ACT broken right now?**<br>
  No. Make sure you have the latest FFXIV plugin by going to the About tab and clicking `Check Version Now`. It will
  most likely update your FFXIV plugin after which you'll have to restart ACT.

  If it doesn't update automatically, go to your Plugins tab and select the `FFXIV_ACT_Plugin.dll`, and check the
  `FileVersion:` on the right side. If it doesn't say `2.0.6.5`, you have an outdated version.
  Try manually updating by [downloading the plugin from Ravahn's repo](https://github.com/ravahn/FFXIV_ACT_Plugin/releases).

* **Is ACT broken right now?**<br>
  Yes. The network opcodes have changed and the parser's network mode won't work until it's updated.<br>
  There's a beta available (below) if you're impatient.

* **When will the parser be updated?**<br>
  It's done when it's done:tm:. Updates are usually available within a few days after a game update.
  Sometimes the parser updates faster.
  I'll link an update here when it's available (and I'm awake).

* **Where can I find the beta and how do I install it?**<br>
  Join [the Discord](https://discord.gg/ahFKcmx) and check the pins in the #beta-testing channel.

  Download the archive you find there and replace your current plugin `.dll` with the one from the archive.
  You can find the location of your current plugin `.dll` by going to ACT's Plugins tab and selecting the
  `FFXIV_ACT_Plugin.dll` entry. The file location will show on the right.

  If you're not confident or encounter any issues while replacing the plugin, wait for the official update
  and install that. This release is used to test if the parser works. Please submit any issues you find (incorrect
  data, missing data, etc.) to the Discord.
-->

## TOC

* Troubleshooting stuff
  - [My ACT isn't showing any numbers. What can I do?](#my-act-isnt-showing-any-numbers-what-can-i-do)
  - [My overlay isn't updating / not showing](#my-overlay-isnt-updating--not-showing)
  - [My overlay only shows if I'm out of the game / alt-tabbed](#my-overlay-only-shows-if-im-out-of-the-game--alt-tabbed)
  - [My overlay shows over the game but stops updating](#my-overlay-shows-over-the-game-but-stops-updating)
  - [My overlay doesn't sort by DPS](#my-overlay-doesnt-sort-by-dps)
  - [OverlayPlugin failed because it couldn't download something](#overlayplugin-failed-because-it-couldnt-download-something)
  - [OverlayPlugin complains that Newtonsoft.Json is outdated](#overlayplugin-complains-that-newtonsoftjson-is-outdated)
  - [OverlayPlugin complains that SharpCompress is outdated](#overlayplugin-complains-that-sharpcompress-is-outdated)
  - [Cactbot's config tab is empty](#cactbots-config-tab-is-empty)
* General questions
  - [How do I install OverlayPlugin or Cactbot?](#how-do-i-install-overlayplugin-or-cactbot)
  - [How do I check my plugin versions?](#how-do-i-check-my-plugin-versions)
  - [Where are the log files saved?](#where-are-the-log-files-saved)
  - [Which OverlayPlugin fork am I supposed to use?](#which-overlayplugin-fork-am-i-supposed-to-use)
  - [Where can I find any documentation on the log file?](#where-can-i-find-any-documentation-on-the-log-file)
* [Glossary](#glossary)
* [Overlays](#overlays)

## Troubleshooting stuff

### My ACT isn't showing any numbers. What can I do?

Go to Plugins > FFXIV Settings and click `Test game connection`.

* **It complains about the firewall. What should I do?**<br>
  Make sure you have a firewall exception for ACT. Also make sure that the
  `.exe` file (visible under Details) and network type are correct.

  If you're sure the firewall exception is correct, disable the firewall. If that fixes your
  problem, your exception is not correct. If that doesn't fix your problem,
  come to [the Discord](https://discord.gg/ahFKcmx) and mention that your parser doesn't work
  even when your firewall is disabled.

* **It complains about memory signatures/addresses. What should I do?**<br>
  This usually means your parser doesn't work with your game version. Check the
  [plugin page](https://github.com/ravahn/FFXIV_ACT_Plugin/releases)
  for updates. If you already have the latest version, you'll probably see a notice at the top
  of this FAQ that an update is being worked on.

  If you got this error with the latest parser and the game hasn't been updated in the last several days,
  go to [the Discord](https://discord.gg/ahFKcmx) and ask for help.

* **It complains that it can't find the game process.**<br>
  Make sure you're running the correct ACT `.exe`. `Advanced Combat Tracker.exe` for the game in DirectX 11
  mode (the default) and `ACTx86.exe` for the game in DirectX 9 mode.

* **It complains that no recent network traffic has been received.**<br>
  Check if your firewall is interfering with the parser or if your VPN is causing problems.

  If you use a VPN, try disabling the "High performance network parser". Disabling it means ACT will cause
  more CPU load but it might fix your problem.

### My overlay isn't updating / not showing

First, check if your FFXIV plugin is the first entry in your plugins list (you can find that on ACT's Plugins tab). If it isn't move it to the top using the arrows and restart ACT. If that didn't fix your issue, continue reading.

Make sure that ACT is showing DPS info on the Main tab. If that doesn't work, you'll have to fix
ACT / the parser first. See the [above section](#my-act-isnt-showing-any-numbers-what-can-i-do) for more information
about that.

Next, check the overlay log if it contains any of the following messages. The overlay log is the area below
your overlay settings.

* `System.NullReferenceException - Object reference not set to an instance of an object.`<br>
  Remove your current OverlayPlugin (delete the files and the folder you *should* have created for the plugin), restart ACT, click the `Get Plugins` button on the Plugins tab and select OverlayPlugin from that list. This will install the latest OverlayPlugin for you.
* `Could not load type 'RainbowMage.OverlayPlugin.EventSourseBase' from assembly 'OverlayPlugin.Core, ...'`<br>
  You tried to use an addon or plugin which requires a newer version of OverlayPlugin, but you are using an obsolete fork.

  You either have to look for a different download / build of the addon/plugin you're trying to use or
  switch to the newest OverlayPlugin.
* `System.TypeLoadException - Could not load type 'System.ValueTuple``3' from assembly 'System.ValueTuple, ...`<br>
  Update your .NET framework to 4.7.1 or newer.

Finally, here are some typical issues which can lead to an overlay showing up but not updating:

* Remove your current overlay, click `New` and select the overlay from the preset list. That should fix any issues related to a wrong URL, ACTWS setting, etc.
* If you're using hibiyasleep's or ngld's OverlayPlugin, uninstall it and install the newest version.
* If you're using the main OverlayPlugin fork, load it directly after the `FFXIV_ACT_Plugin.dll` to make sure no other plugin conflicts with it.
* If you're trying to use MopiMopi or SkillDisplay with the mainline version, make sure you check the ACTWS checkbox.<br>
  If you're using *any* other overlay, uncheck that box since it can break overlays which don't support ACTWS (like Cactbot).
* Certain overlays like MopiMopi don't work with the hibiyasleep version.

### My overlay only shows if I'm out of the game / alt-tabbed

Set your game to run in Borderless mode. Fullscreen means the game has exclusive control of your screen and other
programs can't draw over it.

Discord, Steam, etc. get around this by hooking into the game. We're trying to avoid this which is why we use windows
to draw over the game.

* But it worked before ?!<br>
  Yeah, that was Windows doing some black magic. Essentially, it forced the game into a mode similar to Borderless.
  For some reason, this has been disabled in a recent Windows update.

### My overlay shows over the game but stops updating

This is usually an issue with AMD's graphics driver. Make sure you disable AMD Chill or come to
[the Discord](https://discord.gg/ahFKcmx) and ask for help there.

### My overlay doesn't sort by DPS

You have to enable sorting. Go to `Plugins` > `MiniParseEventSource` and set `Sort By` to `DPS`.

### OverlayPlugin failed because it couldn't download something

Go to the OverlayPlugin tab. It'll tell you more about the file it tried to download. You'll be able to retry the download or manually download the required file there.

### OverlayPlugin complains that Newtonsoft.Json is outdated

Go to your ACT folder (that's where your `Advanced Combat Tracker.exe` is) and delete `Newtonsoft.Json.dll`. That file isn't part of ACT and most likely ended up there as part of a plugin. Please install plugins in `%AppData%\Advanced Combat Tracker\Plugins` or sub folders to avoid issues like this.

If OverlayPlugin still complains about `Newtonsoft.Json` even after you deleted that file, make sure that it's loaded before ACTWebSocket and Discord Triggers and any other plugin that might contain an old version of `Newtonsoft.Json`.
If you need help locating the currently loaded version of `Newtonsoft.Json`, go to ACT's Plugins tab and click `View Loaded Assemblies` on the right side. It'll list all currently loaded assemblies and should show you the path to the currently loaded `Newtonsoft.Json.dll`.

[Join the Discord](https://discord.gg/ahFKcmx) if you need further assistance.

### OverlayPlugin complains that SharpCompress is outdated

Disable ACTWebSocket or load OverlayPlugin before ACTWebSocket. If that doesn't help, check if you have a `SharpCompress.dll` file in your ACT folder (the folder that contains `Advanced Combat Tracker.exe`) and delete it.
Check the above section for further info since it's the same problem just a different file.

### Cactbot's config tab is empty

Check if your overlay log (the text box below your overlay settings) contains an error complaining about an outdated version of `Newtonsoft.Json`. If it does, [follow the instructions above](#overlayplugin-complains-that-newtonsoftjson-is-outdated).
If it doesn't, make sure you updated all of Cactbot's files (and not just the DLL or `ui` folder). If that doesn't help either, [join the Discord](https://discord.gg/ahFKcmx).

## General questions

### How do I install OverlayPlugin or Cactbot?

Go to ACT's Plugins tab and click the `Get Plugins` button. Select the plugin you want from that list. If ACT complains during the Cactbot installation that it doesn't contain a plugin interface, then you have to update your OverlayPlugin first. The easiest way to do that is to completely remove your current OverlayPlugin and then add it again through the `Get Plugins` button.

### How do I check my plugin versions?

Go to the Plugins tab, click on the plugin you want to check and look on the right side for `FileVersion:`.
Next to that label, it will tell you the plugin version.

### Where are the log files saved?

Go to Plugins > FFXIV Settings and look for the `Log file location`. 

The default location is `%appdata%\Advanced Combat Tracker\FFXIVLogs`. 
If you have not customized the location, you can paste this into your start menu for quick access.

### Which OverlayPlugin fork am I supposed to use?

The correct version of OverlayPlugin is the [one in the OverlayPlugin org](https://github.com/OverlayPlugin/OverlayPlugin).
Neither the hibiyasleep nor ngld versions are currently maintained.

### What is ACTWS and how does it relate to OverlayPlugin?

ACTWS was an older solution for exposing a WebSocket to transfer live data out of ACT.
OverlayPlugin has since absorbed all of its functionality, making it obsolete.

### Where can I find any documentation on the log file?

[Cactbot's log guide](https://github.com/quisquous/cactbot/blob/master/docs/LogGuide.md) is the best we currently
have. We don't have any real documentation on the parser itself but feel free to ask on Discord if you have any
specific questions.

## Glossary

* [ACT, Advanced Combat Tracker](https://advancedcombattracker.com/)<br>
  This program offers the core functionality by calculating DPS, HPS, etc. based on a log file.
* [ACTWS, ACTWebSocket](https://github.com/ZCube/ACTWebSocket/releases)<br>
  This plugin runs a web server which accepts WebSocket connections which allows other applications to use ACT's data.
  Not maintained anymore. Most of the functionality has been integrated into ngld's OverlayPlugin.
* [Cactbot](https://github.com/quisquous/cactbot)<br>
  A collection of various overlays. Raidboss can show you timelines for boss fights and dungeons, the eureka overlay
  can show you points of interest for eureka, oopsyraidsy can show you certain mistakes and why people die.
* [FFXIV ACT plugin](https://github.com/ravahn/FFXIV_ACT_Plugin/releases)<br>
  This plugin contains the FFXIV parser for ACT (there are other plugins which allow ACT to parse the data for other
  games). It captures the network packets sent/received by the game and additional data from memory and writes that
  information to a log file. ACT then reads that file and parses it with help from the plugin.
* [FFLogs](http://fflogs.com/)<br>
  A website that allows you to upload the raw network logs and aggregates them.
* [Hojoring](https://github.com/anoyetta/ACT.Hojoring), Special Spell Timers, Yukkuri, UltraScouter<br>
  Hojoring is a collection of the following three plugins:
  + SpecialSpellTimer<br>
    Oversee skill cooldowns, trigger notifications for enemy actions, timeline for raids, etc.
  + Yukkuri<br>
    Replaces ACT's Text to Speech engine. Can interface with most TTS engines currently available.
  + UltraScouter<br>
    Extended HUD. Can display enemy HP values, remaining cast time, distance and direction of hunt marks, threat
    visualization, etc
* [OverlayPlugin](https://github.com/OverlayPlugin/OverlayPlugin)<br>
  This plugin is used for most overlays. It effectively runs a Chromium browser in the background to render
  web pages on top of the game. Various information like the current DPS values are forwarded by the plugin to the
  web page to display.
* Parser<br>
  See **FFXIV ACT plugin** above.
* Triggers<br>
  A trigger allows you to define a certain action (showing an overlay, playing a sound, starting/stopping an OBS
  recording, ...) that should happen whenever a certain thing happens in the game. Very powerful but requires a solid
  understanding of regular expressions and log lines.
* [Triggernometry](https://github.com/paissaheavyindustries/Triggernometry)<br>
  More or less replaces ACT's Custom Triggers feature with a much more capable version. For example, variables and
  conditions are supported, as well as visual warnings and callouts (auras).

  The plugin is a toolbox for building your own things for whatever calls and situations you like,
  and as such it does not contain any triggers out of the box. You can, however, find people sharing their
  creations through the plugin's remote repos feature or on [Triggernometry's Discord server](https://discord.gg/6f9MY55)
  where you will also be able to find assistance in building your own things.

Disclaimer: A few of the above plugin descriptions have been taken from the FFXIV Discord's #plugin-showcase.

## Overlays

**If you have the latest OverlayPlugin, take a look at the different presets it offers** (click the `New` button on the OverlayPlugin.dll tab). **That list is more complete and includes previews.**

Triggernometry, SpecialSpellTimers and UltraScouter can also display additional information on top of the game.

*TODO:* Add updated screenshots for all of these. Would probably more useful than the text descriptions.

However, pure DPS data / DPS tables are usually displayed by one of these:

* [Kagerou](https://hibiyasleep.github.io/kagerou/overlay/), [README link](https://github.com/hibiyasleep/kagerou)<br>
  A very popular overlay displaying DPS, damage taken and HPS. Has a lot of options to customize the displayed data
  and overall look and feel. Works with all overlay renderers.

  ![](https://gist.github.com/ngld/e2217563bbbe1750c0917217f136687d/raw/44edc533a40757e7bb6faf30ea1b73d347823d7e/Kagerou.png)
* [MopiMopi](https://haeruhaeru.github.io/mopimopi/), [README link](https://github.com/haeRUHAERU/mopimopi)<br>
  Also fairly popular. Displays DPS and HPS. Doesn't group the data into tabs and instead displays both tables
  next to each other. Requires ngld's OverlayPlugin or ACTWebSocket.

  ![](https://gist.github.com/ngld/e2217563bbbe1750c0917217f136687d/raw/44edc533a40757e7bb6faf30ea1b73d347823d7e/MopiMopi.png)
* a modified version of RainbowMage<br>
  RainbowMage created OverlayPlugin and the first overlay that worked with it. Since then multiple modified versions
  have been created. [This repo contains a pretty broad selection and additional
  overlays](https://github.com/billyvg/OverlayPlugin-themes/).

  Works with both hibiyasleep and ngld OverlayPlugin.
* [Ember](https://goldenchrysus.github.io/ffxiv/ember-overlay/), [README
  link](https://github.com/GoldenChrysus/ffxiv-ember-overlay)<br>
  This overlay tries to follow FFXIV's overall UI design and offers a bunch of data.<br>
  Works with all overlay renderers.
* [Horizoverlay](https://bsides.github.io/horizoverlay/), [README link](https://github.com/bsides/horizoverlay)<br>
  A simple horizontal damage meter overlay. It currently shows player dps, damage %, hps, encounter duration and total dps.
  Works with OverlayPlugin 0.3.3.13 or newer (both hibiysleep and ngld).
* [Ikegami](https://idyllshi.re/ikegami/), [README link](https://github.com/hibiyasleep/ikegami)<br>
  A simple horizontal miniparse overlay. Works with all overlay renderers.

  ![](https://gist.githubusercontent.com/ngld/e2217563bbbe1750c0917217f136687d/raw/44edc533a40757e7bb6faf30ea1b73d347823d7e/Ikegami.png)
