# Home Assistant

My personal Home Assistant (HA) configuration.

## Software

* HA: 0.117 ([details](https://www.home-assistant.io/blog/2020/10/28/release-117/))
* Companion App (iOS): 2020.6 ([details](https://github.com/home-assistant/iOS/releases/tag/testflight%2F2020.6%2F15))

![](https://media1.tenor.com/images/f2fb267ad09005a703a2347e3521fa70/tenor.gif?itemid=7288512)

Each time I upgrade HA feels like last act of *The Good, the Bad and the Ugly*... I mean, HA updates [remove useful core components](https://hasspodcast.io/ha033/) and or [break custom components compatibility](https://community.home-assistant.io/t/custom-header/155399/1100).

## Custom components this configuration has

There are many HA configuration repositories and the mayor difference is the theme and views/cards arrangement. Here are the custom components that you only will see in my personal configuration -- hope you like them!

I recommend [imgbb](https://imgbb.com) to save screenshots.

### Real uptime

If you want to count the days [since the last boot](https://www.home-assistant.io/integrations/systemmonitor/), take a look at "*Uptime*" sensor (in *sensors.yaml*).

![](https://i.ibb.co/g7m9jLB/Screen-Shot-2020-09-20-at-21-30-02.png)

### Pihole integration

Pihole switch was added in [release 0.114](https://www.home-assistant.io/blog/2020/08/12/release-114/#breaking-changes) but isn't *smart* when you disable the service for a given time. After the given time is reached the switch appears as *off*.

![](https://i.ibb.co/vxmD0BC/Screen-Shot-2020-09-20-at-21-26-37.png)

To fix it, take a look at "*PiHole status*" sensor (in *sensors.yaml*) and "*Enable Pihole again*" automation (in *automations.yaml*).

Also, you will find "*Pihole versions*" sensor (in *sensors.yaml*) to get the installed and latest version of each Pihole component (Core, Web UI and FTL).

### Astronomy API

I use [IPGeolocation's Astronomy API](https://ipgeolocation.io/documentation/astronomy-api.html) to get the location-based rise and set times for the Sun and the Moon and day length. Take a look at "*Astronomy API*" sensor (in *sensors.yaml*).

Do not forget to use "*scan_interval: 90*" if you will use the free plan, it will do 960 requests/day to avoid 1K daily limit.

### Broadlink send command

If you have two or more Broadlink RM device, you can reuse the learned commands for all devices. Take a look at "*broadlink_send_command*" script (in *script.yaml*) and "*broadlink_codes*" sensor (in *sensors.yaml*).

This solution is based on [a comment from HA Community's](https://community.home-assistant.io/t/41792/9).

### Wind direction compass

If you have a weather station, I made a sensor to convert wind direction's degree in cardinal direction and also it changes the icon based on direction.

![](https://i.ibb.co/LrqkkhH/Screen-Shot-2020-08-29-at-15-52-13.png)

Take a look at "*Wind direction*" sensor (in *sensors.yaml*) and entity configuration in *views/weather.yaml*.

### Radio on Google Chromecast / Home

Listen to your favorite radio in one or all of your Google speakers.

![](https://i.ibb.co/LNSncNP/Screen-Shot-2020-09-20-at-21-17-50.png)

It uses many components, take a look at names that contain "speakers" or "radio" (in *configuration.yaml*, *automations.yaml*, *input_select.yaml* and *scripts.yaml*).

This solution is based on [Chromecast Radio with station and player selection](https://community.home-assistant.io/t//12732)

### Raspbian upgradeable packages sensor

Based on [HACS' pending updates sensor](https://hacs.xyz/docs/basic/sensor) I made a sensor to list upgradeable packages candidates for Raspbian OS.

![](https://i.ibb.co/p3mm9SX/1601517839.png)

Take a look at "*Raspbian*" sensor (in *sensors.yaml*).

Command has many backslash to scape characters in YAML, if you want to reuse it and/or try in your shell, run

```
apt list --upgradeable | \
sed -e 1d | \
sed -n 's!^\([^/]*\)/[^0-9]*\([^ ]*\) [a-z].*: \([^]]*\)]!{ "name": "\1", "installed_version": "\3", "available_version": "\2" },!p' | \
sed -e '1s/^/{ "packages": [/' -e '$s/},/}] }/'
```

## Hardware

* [Raspberry Pi 3 Model B+](https://static.raspberrypi.org/files/product-briefs/200206+Raspberry+Pi+3+Model+B+plus+Product+Brief+PRINT&DIGITAL.pdf)
* [Sonoff Basic R2](https://sonoff.tech/product/wifi-diy-smart-switches/basicr2)
* [Sonoff POW R2](https://sonoff.tech/product/wifi-diy-smart-switches/powr2)
* [Sonoff TH16](https://sonoff.tech/product/wifi-diy-smart-switches/th10-th16)
* [Sonoff TX series](https://sonoff.tech/product/wifi-smart-wall-swithes/tx-series)
* [Sonoff iFan03](https://sonoff.tech/product/wifi-diy-smart-switches/ifan03)
* [Google Home Mini (1st Gen)](https://store.google.com/us/product/google_home_mini_first_gen?hl=en-US)
* [Google Chromecast Audio](https://www.pcmag.com/reviews/google-chromecast-audio) (discontinued)
* [Ambient Weather WS-2902A](https://www.lifewire.com/ambient-weather-ws-2902a-osprey-review-4766784) (discontinued)
* [Broadlink RM Pro+](https://www.banggood.com/Broadlink-RM-Pro-Smart-Home-Automation-Phone-Wireless-Remote-Universal-Controller-EU-Plug-p-942667.html) (discontinued)
* [Tuya smart plug](https://cnshinelite.en.made-in-china.com/product/IdiQrUOYhakB/China-Tuya-APP-Au-Type-Electrical-Smart-Plug-for-Smart-Home.html) (in South America sold by Nex/Cencosud S.A. brand)
* [Xiaomi MiJia vacuum cleaner](https://xiaomi-mi.com/cleaning-gear/xiaomi-mijia-roborock-robot-vacuum-cleaner-white/)

Will be added:

* [ARILUX SL-LC 04 LED controller](https://www.banggood.com/ARILUX-SL-LC-04-Super-Mini-LED-WIFI-APP-Controller-+-Remote-Control-For-RGBW-LED-Strip-DC-9-12V-p-1060231.html)

## Integrations

* [HACS](https://hacs.xyz)
* [Sonoff LAN](https://github.com/AlexxIT/SonoffLAN)
* [SmartIR](https://github.com/smartHomeHub/SmartIR)

## Addons

* [Button Card](https://github.com/custom-cards/button-card)
* [state-switch](https://github.com/thomasloven/lovelace-state-switch)
* [multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row)

## Themes

* [Dark Teal](https://github.com/aFFekopp/dark_teal)

## Extra notes

Take a look at [Tips](/utils/README.md#Tips) and [Troubleshooting](/utils/README.md#Troubleshooting).
