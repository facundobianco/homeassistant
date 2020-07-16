# Home Assistant

My personal home assistant configuration.

<img src="https://i.ibb.co/XSJvXv3/IMG-4976.png" width="209.95" height="363.35">&nbsp;&nbsp;&nbsp;<img src="https://i.ibb.co/tM1wwbZ/IMG-4977.png" width="209.95" height="363.35">&nbsp;&nbsp;&nbsp;<img src="https://i.ibb.co/k9vG75C/IMG-4978.png" width="209.95" height="363.35">

Images stored in [imgbb <img src="https://simgbb.com/images/favicon.png" width="16" height="16">](https://imgbb.com)

## Required external packages

* [monitoring-plugins-basic](https://packages.debian.org/buster/monitoring-plugins-basic) (plugins for Nagios compatible monitoring systems)

## Integrations

* Browser mod
* HACS
* Sonoff LAN

## Pluginsx

* Circle Sensord Card
* Custom header
* Fan controller entity row
* Mini Graph card
* Mini Media Player
* button-card
* card-mod
* layout-card
* state-switch

## Themes

* Dark Teal

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

## Recommended links

* [Atom IDE: Edit remote files using SSH/FTP](https://atom.io/packages/remote-edit-ni)
