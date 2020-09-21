# Home Assistant

My personal Home Assistant (HA) configuration.

## Software

* HA: 0.115 ([details](https://www.home-assistant.io/blog/2020/09/17/release-115/))
* Companion App (iOS): 2020.6 ([details](https://github.com/home-assistant/iOS/releases/tag/testflight%2F2020.6%2F15))

<img src="https://media1.tenor.com/images/f2fb267ad09005a703a2347e3521fa70/tenor.gif?itemid=7288512" />

Each time I upgrade HA feels like last act of *The Good, the Bad and the Ugly*...

## Custom components this configuration has

There are many HA configuration repositories and the mayor difference is the theme and views/cards arrangement. Here are the custom components that you only will see in my personal configuration -- hope you like them!

I recommend [imgbb](https://imgbb.com) to save screenshots.

### Real uptime

If you want to count the days [since the last boot](https://www.home-assistant.io/integrations/systemmonitor/), take a look at "*Uptime*" sensor (in *sensors.yaml*).

<img src="https://i.ibb.co/0jchZpg/Screen-Shot-2020-09-20-at-21-30-02.png" width="50%" />

### Pihole integration

Pihole switch was added in [release 0.114](https://www.home-assistant.io/blog/2020/08/12/release-114/#breaking-changes) but isn't *smart* when you disable the service for a given time. After the given time is reached the switch appears as *off*.

<img src="https://i.ibb.co/0rxWtCW/Screen-Shot-2020-09-20-at-21-26-37.png" width="50%"  />

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

<img src="https://i.ibb.co/4RmpKyG/Screen-Shot-2020-08-29-at-15-52-13.png" alt="Screen-Shot-2020-08-29-at-15-52-13"  width="50%" />

Take a look at "*Wind direction*" sensor (in *sensors.yaml*) and entity configuration in *views/weather.yaml*.

### Radio on Google Chromecast / Home

Listen to your favorite radio in one or all of your Google speakers.

<img src="https://i.ibb.co/hHn3x04/Screen-Shot-2020-09-20-at-21-17-50.png"  width="50%" />

It uses many components, take a look at names that contain "speakers" or "radio" (in *configuration.yaml*, *automations.yaml*, *input_select.yaml* and *scripts.yaml*).

This solution is based on [Chromecast Radio with station and player selection](https://community.home-assistant.io/t//12732)

## Hardware

* [Raspberry Pi 3 Model B+](https://static.raspberrypi.org/files/product-briefs/200206+Raspberry+Pi+3+Model+B+plus+Product+Brief+PRINT&DIGITAL.pdf)
* [Sonoff Basic R2](https://sonoff.tech/product/wifi-diy-smart-switches/basicr2)
* [Sonoff POW R2](https://sonoff.tech/product/wifi-diy-smart-switches/powr2)
* [Sonoff TH16](https://sonoff.tech/product/wifi-diy-smart-switches/th10-th16)
* [Sonoff TX series](https://sonoff.tech/product/wifi-smart-wall-swithes/tx-series)
* [Sonoff iFan03](https://sonoff.tech/product/wifi-diy-smart-switches/ifan03)
* [Ambient Weather WS-2902A](https://www.lifewire.com/ambient-weather-ws-2902a-osprey-review-4766784) (discontinued)
* [Broadlink RM Pro+](https://www.banggood.com/Broadlink-RM-Pro-Smart-Home-Automation-Phone-Wireless-Remote-Universal-Controller-EU-Plug-p-942667.html) (discontinued)
* [Tuya smart plug](https://cnshinelite.en.made-in-china.com/product/IdiQrUOYhakB/China-Tuya-APP-Au-Type-Electrical-Smart-Plug-for-Smart-Home.html) (in South America sold by Nex/Cencosud S.A. brand)

## Integrations

* [HACS](https://hacs.xyz)
* [Sonoff LAN](https://github.com/AlexxIT/SonoffLAN)
* [SmartIR](https://github.com/smartHomeHub/SmartIR)

## Addons

* [Custom header](https://github.com/maykar/custom-header)
* [Fan control entity row](https://github.com/finity69x2/fan-control-entity-row)
* [Button Card](https://github.com/custom-cards/button-card)
* [state-switch](https://github.com/thomasloven/lovelace-state-switch)
* [multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row)

## Themes

* [Dark Teal](https://github.com/aFFekopp/dark_teal)

## Required external packages

Will be replaced by script (ASAP).

* [monitoring-plugins-basic](https://packages.debian.org/buster/monitoring-plugins-basic) (plugins for Nagios compatible monitoring systems)

## Tips

### Load secrets

There are two ways to load secrets in YAML and/or Jinja2 lines.

The simplest one is using *input_text*

```
input_text:
  foo:
    initial: !secret foo
```

Other way is storage secrets as sensor's attribute, then can be loaded based in a *input_select*'s value. Add a new template sensor as

```
- platform: template
  sensors:
    foo:
      value_template: "OK"
      attribute_templates:
        item1: !secret foo_secret1
        item2: !secret foo_secret2
        itemN: !secret foo_secretN
```

And load them as

```
{{ state_attr('sensor.foo', input_select_item) }}
```

### Use metric system

If one of your sensors doesn't use the metrics system, create a custom one and add a math formula in *value_template*.

To convert inHg (*inch of mercury*) to hPa (*hectopascal*):

```
value_template: >-
  {% set val = float(states('sensor.pressure')) %}
  {{ (val / 0.029529983071445) | round(2) }}
```

To convert inches to millimeters:

```
value_template: >-
  {% set val = float(states('sensor.inches')) %}
  {{ (val * 25.4)  | round(2) }}
```

To convert mi/h (*miles per hour*) to km/h (*kilometers per hour*)

```
value_template: "{{ (states('sensor.speed') | float * 1.609) | round(2) }}"
```

### Edit remote files

I recommend Atom IDE with package [remote-edit-ini](https://atom.io/packages/remote-edit-ni).

In *status-bar* you will see the long, long temporary file's path and it's annoying because hides the cursor position. To avoid that, add in *styles.less* configuration file

```
// Hide path in status-bar
status-bar {
  .current-path {
    display: None;
  }
}
```

## Troubleshooting

### Custom Header exception in iOS

In HA >= 0.111 *Custom Header* component ignores the user agent exception for iOS application.

Solution is

```
- conditions:
    media_query: "(max-width: 375px)"
```

To get your iOS width, visit [whatismyscreenresolution.net](http://whatismyscreenresolution.net).

### HACS: Warning about community_plugin

For version >= 0.107 you will find this warning message:

> WARNING (MainThread) [hacs.deprecated] The '/community_plugin/*' is deprecated and will be removed in an upcomming version of HACS, it has been replaced by '/hacsfiles/*'

To solve it, [edit plugins location](https://community.home-assistant.io/t/0-107-warning-about-community-plugin/179511/2).

### Custom element doesn't exist

If you get the *red card* with the message "Custom element doesn't exist: foo.", just delete cookies, website data and refresh a few times. Source: [HA Community](https://community.home-assistant.io/t/custom-element-doesnt-exist/91942/6).

### Unable to import libopenjp2.so.7

If you get the error message

> ERROR (MainThread) [homeassistant.setup] Setup failed for image: Unable to import component: libopenjp2.so.7: cannot open shared object file: No such file or directory

run

```
apt install -y libopenjp2-7
```
