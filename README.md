# Home Assistant

My personal home assistant configuration.

<img src="https://i.ibb.co/4sGsH3X/IMG-5341.png" width="209.95" height="363.35">&nbsp;&nbsp;&nbsp;<img src="https://i.ibb.co/8Y71kxw/IMG-5342.png" width="209.95" height="363.35">&nbsp;&nbsp;&nbsp;<img src="https://i.ibb.co/X8qvsS2/IMG-5340.png" width="209.95" height="363.35">

Images stored in [imgbb <img src="https://simgbb.com/images/favicon.png" width="16" height="16">](https://imgbb.com)

## Integrations

* [HACS](https://hacs.xyz)
* [Sonoff LAN](https://github.com/AlexxIT/SonoffLAN)

## Plugins

* [Custom header](https://github.com/maykar/custom-header)
* [Fan control entity row](https://github.com/finity69x2/fan-control-entity-row)
* [Button Card](https://github.com/custom-cards/button-card)
* [state-switch](https://github.com/thomasloven/lovelace-state-switch)
* [multiple-entity-row](https://github.com/benct/lovelace-multiple-entity-row)

## Themes

* [Dark Teal](https://github.com/aFFekopp/dark_teal)

## Required external packages

* [monitoring-plugins-basic](https://packages.debian.org/buster/monitoring-plugins-basic) (plugins for Nagios compatible monitoring systems)

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

## Recommended links

* [Atom IDE: Edit remote files using SSH/FTP](https://atom.io/packages/remote-edit-ni)
