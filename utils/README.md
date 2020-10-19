# Utilities

This directory contains files related to HA.

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

I recommend Atom IDE with packages

* [platformio-ide-terminal](https://atom.io/packages/platformio-ide-terminal)
* [remote-edit-ini](https://atom.io/packages/remote-edit-ni)

Using *remote-edit-ini* in status bar you will see the long, long temporary file's path and it's annoying because hides the cursor position. To avoid that, add in *styles.less* configuration file

```
// Hide path in status-bar
status-bar {
  .current-path {
    display: None;
  }
}
```

## Updates

### Home Assistant

```
ha-stop
source virtualenv/bin/activate
pip install --upgrade homeassistant
deactivate
ha-start
```

### Pihole

Check the upgrade status

```
pihole -up --check-only
```

And upgrade it

```
pihole -up
sed -i '/^server.port/s/80/&80/' /etc/lighttpd/lighttpd.conf
systemctl start lighttpd
```

### Certbot SSL

```
systemctl stop nginx.service
certbot renew
systemctl start nginx.service
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

### Google Assistant: homegraph API error 403

Every time you update [Google entities](https://www.home-assistant.io/integrations/google_assistant/#entity_config) you will get the error message

> [homeassistant.components.google_assistant.http] Request for https://homegraph.googleapis.com/v1/devices:reportStateAndNotification failed: 403

Open your Google Home application and say "sync my devices". Error message is gone. Source: [HA Community](https://community.home-assistant.io/t/148289/16).
