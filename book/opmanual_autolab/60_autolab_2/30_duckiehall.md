# Duckiehall {#autolab-2-duckiehall status=draft}

<div class='requirements' markdown="1">

Requires: An Raspberry Pi 4

Results: A Duckiehall for the Duckietown in the Autolab

</div>


Note: `RPi4` refers to the Raspberry Pi 4


## What is a Duckiehall?

Logically, a Duckiehall robot oversees the communications in a Duckietown. So there is one Duckiehall per Duckietown. Since the Duckiehall robot only does computations and does not have actuators or sensors, it is simply a RPi4 connected to the same network as the other robots in the Duckietown.


## Initialize

### Flash the SD card

The parameters:

* `concat_map_name` should be the name of the map for this Duckietown merged in the `duckietown/duckietown-world` Github repository, but concatenated over the underscore("_")s. E.g. For map name `ETH_large_loop`, the `concat_map_name` is `ETHlargeloop`.
* `country_code` is the [two-letter country code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)

Command to flash:

    laptop $ dts init_sd_card --hostname ![concat_map_name] --type duckietown --configuration DT21 --country ![country_code]


### Connect to network and boot

The network connection should be wired. Insert the SD card to the RPi4 and power the RPi4 on. Check the boot finished if the Duckiehall showed up in:

    laptop $ dts fleet discover


## Setup

### Navigate to the Duckiehall dashboard and login

<div figure-id="fig:dashboard-login">
<img src="opmanual_autolab/images/autobots_dashboard-login.png" style="width: 80%"/>
</div>

### Select "Settings" pane

<div figure-id="fig:dashboard-settings">
<img src="opmanual_autolab/images/autobots_dashboard-settings.png" style="width: 80%"/>
</div>

### Fill in the configs for "Autolab"

<div figure-id="fig:dashboard-autolab-config">
<img src="opmanual_autolab/images/autobots_dashboard-autolab-config.png" style="width: 80%"/>
<figcaption style="text-align: center">
Check below for what values to fill
</figcaption>
</div>

The "Map name" field requires a string, e.g. `ETH_large_loop`. It's the name of the map of the Duckietown created and merged to the `duckietown/duckeitown-world` Github repository.

Note: pay attention to the difference between "Map name" and `concat_map_name` mentioned when initializing the SD card. 

Note: The "Tag id" field should be omitted for a Duckiehall robot.

Click "Save and Apply" and refresh the page. The user inputs should appear in the fields now.
