# Xbox One support for Home Assistant

## Dependencies

Requires running [Xbox One Smartglass REST server](https://github.com/OpenXbox/xbox-smartglass-core-python).

HASS.io users can use the official addon: [Check it out](https://github.com/OpenXbox/xboxone-home-assistant)

## Features

This component replicates many of the features of the Xbox App.  If it can't be done there, it can't be done here.

- Power On/Off
- Display name and image of current Game/App
  - Requires auth with Xbox Live
- Media Controls: Play/Pause & Seek
  - Supported apps only
- Volume Controls: Up/Down/Mute
  - Requires `Device Control` to be configured in `Settings` on the Xbox
- ~~Source Selection: Launch Pinned Apps from within Home Assistant~~
  - ~~Apps only, Games not supported~~ (Feature was removed by Microsoft via console system update)

## Installation of  the component

There are two ways to do the installation, HACS and manually. HACS is preferred because its more failsafe.

### HACS

1. Install HACS [hacs](https://hacs.xyz/docs/installation/prerequisites).
1. In HACS' __Community tab -> Integrations__ search for __Xbox One - smartglass media player__.
1. Install the component and let Home Assistant restart.

### Manual installation

1. Locate your Home Assistant config directory
1. Copy the folder `custom_components/xboxone` to your `<HOME ASSISTANT CONFIG DIR>/custom_components/xboxone`.
1. Restart Home Assistant.

## Home Assistant Configuration

Follow the below steps to get started.

1. Turn on all of the Xboxes you wish to be discovered.
1. View the device list in this plugin: [hassio.local:5557/device](http://hassio.local:5557/device)
1. Create the `media_player` configuration using the `liveid` as the value for `device`.
1. Restart Home Assistant to pick up the config change.

Example `configuration.yaml`:

```yaml
media_player:
  - platform: xboxone
    device: FD009374623167E
    name: Living Room Xbox One
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `platform`

**Required:** This must be set to `xboxone`

### Option: `device`

The LiveID of your Xbox One.  It can be found in `/device` endpoint.  Once this addon is up and running [click here](http://hassio.local:5557/device).

### Option: `ip_address`

The IP Address of your Xbox One.  Useful if your xbox lives on a separate subnet.

### Option: `name`

The friendly name for this Xbox which will appear in Home Assistant.

### Option: `authentication`

**Default:** `true`

Set to `false` if you have multiple consoles on your network and have issues with getting signed out.  Future features may require an authenticated connection with the console.

**Note:** _This refers to an authenticated connection with the console.  You will still need to [authenticate with Xbox Live](http://hassio.local:5557/auth/oauth) to have the most useful features enabled (i.e. Friendly app names, images, and Source selection).

## Authenticate with Xbox Live

In order to use some of the features listed above, you'll need to sign into Xbox Live.

1. Surf to your Hass.io instance and use port `5557`
    (e.g. `http://hassio.local:5557`).
1. Authenticate by going to [/auth/oauth](http://hassio.local:5557/auth/oauth)
    and following the directions.

## Credits

- Jason Hunter ([@hunterjm](https://github.com/hunterjm)) - Creator of custom component & Hass.io addon
- Eric Leblanc ([@ericleb010](https://github.com/ericleb010)) and [@jmhill1287](https://github.com/jmhill1287) - Maintaining & giving user support
