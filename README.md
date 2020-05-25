# Home Assistant

My personal home assistant configuration.

<img src="https://i.ibb.co/pjd54qZ/5763-C956-0017-46-D3-92-DB-D12-FFBFF50-E2.jpg" width="209.95" height="363.35">&nbsp;&nbsp;&nbsp;<img src="https://i.ibb.co/4Sd9xHy/IMG-2800.jpg" width="209.95" height="363.35">

## Integrations

* Browser mod
* HACS
* Sonoff LAN

## Plugins

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

### HACS: Warning about community_plugin

For version >= 0.107 you will find this warning message:

> WARNING (MainThread) [hacs.deprecated] The '/community_plugin/*' is deprecated and will be removed in an upcomming version of HACS, it has been replaced by '/hacsfiles/*'

To solve it, [edit plugins location](https://community.home-assistant.io/t/0-107-warning-about-community-plugin/179511/2) and do not forget to remove `custom:` in elements installed in HACS.

## Recommended links

* [Atom IDE: Edit remote files using SSH/FTP](https://atom.io/packages/remote-edit-ni)
