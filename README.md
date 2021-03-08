# Home Assistant

My personal Home Assistant (HA) configuration.

## Software

* HA: 2021.3.X ([details](https://www.home-assistant.io/blog/2021/03/03/release-20213))
* Companion App (iOS): 2021.2.2 (55) ([details](https://github.com/home-assistant/iOS/releases/tag/release%2F2021.2.2%2F2021.55))

## Custom components this configuration has

There are many HA configuration repositories and the mayor difference is the theme and views/cards arrangement. Here are the custom components that you only will see in my personal configuration -- hope you like them!

* Real OS uptime
* Pi-hole integration (a switch was added in [release 0.114](https://www.home-assistant.io/blog/2020/08/12/release-114/#breaking-changes) but isn't *smart* when you disable the service for a given time)
* Astronomy API (consuming [IPGeolocation's Astronomy API](https://ipgeolocation.io/documentation/astronomy-api.html))
  * Day length
  * Sun status (Sunrise, Noon and Sunset)
  * Moon status (Moonrise, Lunar Noon and Moonset)
  * Sun & Moon elevation
* Send commands to Broadlink RM device (based on [a comment from HA Community's](https://community.home-assistant.io/t/41792/9))
* Wind direction compass
* Radio on Google Chromecast / Google Home (based on [Chromecast Radio with station and player selection](https://community.home-assistant.io/t//12732))
* Packages pending updates sensor and list them (like [HACS' sensor](https://hacs.xyz/docs/basic/sensor))
  * Raspberry OS (ex Raspbian)
  * Home Assistant core
  * Pi-hole (Core, Web and FTL)
* Upgrade Raspberry OS packages from HA (and updates related sensor)
* Philips Hue integration
  * REST script to send scenes
  * Fully management of dimmer switch using HA
  * *Night mode* if light is turned on in the middle of the night
* Fan management without extra component
* Water boiler management based on hours (turn on) and reached temperature (turn off)

## Hardware

* [Raspberry Pi 3 Model B+](https://static.raspberrypi.org/files/product-briefs/200206+Raspberry+Pi+3+Model+B+plus+Product+Brief+PRINT&DIGITAL.pdf)
* Sonoff
  * [Basic R2](https://sonoff.tech/product/wifi-diy-smart-switches/basicr2)
  * [POW R2](https://sonoff.tech/product/wifi-diy-smart-switches/powr2)
  * [TH16](https://sonoff.tech/product/wifi-diy-smart-switches/th10-th16)
  * [TX series](https://sonoff.tech/product/wifi-smart-wall-swithes/tx-series)
  * [iFan03](https://sonoff.tech/product/wifi-diy-smart-switches/ifan03)
  * [RF Bridge433](https://sonoff.tech/product/accessories/433-rf-bridge)
* Google
  * [Home Mini (1st Gen)](https://store.google.com/us/product/google_home_mini_first_gen?hl=en-US)
  * [Google Chromecast Audio](https://www.pcmag.com/reviews/google-chromecast-audio) (discontinued)
* [Ambient Weather WS-2902A](https://www.lifewire.com/ambient-weather-ws-2902a-osprey-review-4766784) (discontinued)
* [Broadlink RM Pro+](https://www.banggood.com/Broadlink-RM-Pro-Smart-Home-Automation-Phone-Wireless-Remote-Universal-Controller-EU-Plug-p-942667.html) (discontinued)
* [Tuya smart plug](https://cnshinelite.en.made-in-china.com/product/IdiQrUOYhakB/China-Tuya-APP-Au-Type-Electrical-Smart-Plug-for-Smart-Home.html) (in South America sold by Nex/Cencosud S.A. brand)
* [Xiaomi MiJia / Mi Roborock V1 vacuum cleaner](https://xiaomi-mi.com/cleaning-gear/xiaomi-mijia-roborock-robot-vacuum-cleaner-white/)
* Philips Hue
  * [Bridge](https://www.philips-hue.com/en-us/p/hue-bridge/046677458478)
  * [Dimmer Switch](https://www.philips-hue.com/en-us/p/hue-dimmer-switch/046677473372)
  * [White Bulb](https://www.philips-hue.com/en-us/p/hue-white-1-pack-e26/046677476861)
  * [White & Color Bulb](https://www.philips-hue.com/en-us/p/hue-white-and-color-ambiance-1-pack-e26/046677548483)

Will be added:

* [ARILUX SL-LC 04 LED controller](https://www.banggood.com/ARILUX-SL-LC-04-Super-Mini-LED-WIFI-APP-Controller-+-Remote-Control-For-RGBW-LED-Strip-DC-9-12V-p-1060231.html)

## Integrations

* [HACS](https://hacs.xyz)
* [Sonoff LAN](https://github.com/AlexxIT/SonoffLAN)
* [SmartIR](https://github.com/smartHomeHub/SmartIR)
* [Fast-Hue customizer](https://github.com/azogue/fasthue)

## Addons

* [Button Card](https://github.com/custom-cards/button-card)
* [state-switch](https://github.com/thomasloven/lovelace-state-switch)
* [multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row)
* [Simple thermostat card](https://github.com/nervetattoo/simple-thermostat)
* [Paper Buttons Row](https://github.com/jcwillox/lovelace-paper-buttons-row)
* [Vacuum Card](https://github.com/denysdovhan/vacuum-card)
* [card-mod](https://github.com/thomasloven/lovelace-card-mod) (required to [modify background color](https://community.home-assistant.io/t/193638/25) in Vacuum Card)
* [panel-redirect.js](https://gist.github.com/balloob/580deaf8c3fc76948559c5963ed4d436)

## Themes

* [Dark Teal](https://github.com/aFFekopp/dark_teal)

## Extra notes

Take a look at [Tips](/utils/README.md#Tips) and [Troubleshooting](/utils/README.md#Troubleshooting).

## Criticism

Each time I upgrade HA feels like last act of *The Good, the Bad and the Ugly* ([watch here](https://www.youtube.com/watch?v=aJCSNIl2Pls)), you don't know where the bullets will come from... I mean, HA updates is moving from YALM to UI [[1]](https://hasspodcast.io/ha033/)[[2]](https://www.home-assistant.io/blog/2021/03/03/release-20213/#integrations-now-available-to-set-up-from-the-ui) and [breaking custom components compatibility](https://community.home-assistant.io/t/custom-header/155399/1100).
