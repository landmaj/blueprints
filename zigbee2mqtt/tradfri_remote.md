# TRÅDFRI 5-Button Remote

## Binding to light sources from Zigbee2MQTT UI

> [!NOTE]
> Requires firmware version 24.4.5.
> If binding does not work, press any button on the remote to wake it up before attempting to bind.

1. Navigate to `Devices` -> select your TRÅDFRI remote -> `Bind` tab.
1. Remove all binding (if any).
1. Recreate binding with the Coordinator as destination and `genPowerCfg` cluster as the only cluster.
1. Create binding with your desired light entity and select clusters: `genLevelCtrl`, `genOnOff`, `genScenes`.

At this point the remote should be able to toggle the light and change brightness.
For color temperature control you have to create scenes first.

1. Navigate to `Groups` tab and create group with ID `65289`, name does not matter (let's use `tradfri_scenes`).
1. Add your desired light entity to the group.
1. Navigate to `Settings` -> `Dev console` -> `MQTT`.
1. Set the topic to the group name, followed by `/set` (e.g. `tradfri_scenes/set`).
1. Send the following command for each scene you want:

### Cold (4000K)

```json
{
    "scene_add": {
        "ID": 0,
        "name": "cold",
        "state": "ON",
        "color_temp": 250,
        "transition": 1
    }
}
```

### Neutral (3400K)

```json
{
    "scene_add": {
        "ID": 1,
        "name": "neutral",
        "state": "ON",
        "color_temp": 294,
        "transition": 1
    }
}

### Warm (2800K)

```json
{
    "scene_add": {
        "ID": 2,
        "name": "warm",
        "state": "ON",
        "color_temp": 357,
        "transition": 1
    }
}
```

### Warmest (2200K)

```json
{
    "scene_add": {
        "ID": 3,
        "name": "warmest",
        "state": "ON",
        "color_temp": 454,
        "transition": 1
    }
}
```

Tradfri bulbs by default have 3 scenes with IDs 0, 1 and 2. You can `Remove all` scenes
from Zigbee2MQTT UI and even verify by reading cluster `genScenes` attribute `count` that
no scenes exist and yet the bulb will still behave as if those 3 scenes are present.
The only way to get rid of them is to override them by adding new scenes with the same IDs.
