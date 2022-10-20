# Operation: Localization {#autolab-2-localization status=draft}

<div class='requirements' markdown="1">

Requires: Previous sections

Requires: A desktop/laptop machine running Ubuntu (minimum 18.04LTS)

Results: Can run localization experiments

Next Steps: Use this system for AIDO evaluations
</div>

TODO: More specific desktop/laptop hardware requirements

Remark: The desktop/laptop machine is referred to as the main machine. If not specified, the commands should be run from the main machine.

## Basics

### Install docker-compose
On the main machine, follow the official document: [https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


###  Update all robots

Note: For __all__ robots (Autobot, Watchtower, Duckiehall)

Update all containers: 

    $ dts duckiebot update ![hostname]


### On robots, based on the robot type, create some configs:

Warning: __Autobots__ only

Replace `[TAG_ID]` with the Apriltag ID (just number) on top of that Autobot: 

    $ echo ![TAG_ID] > /data/config/autolab/tag_id

Note: For __all__ robots (Autobot, Watchtower, Duckiehall)

Replace `[MAP_NAME]` with the map name for this autolab, e.g. `ETH_large_loop`

    $ echo ![MAP_NAME] > /data/config/autolab/map_name


### Start core container on watchtowers

Warning: __Watchtowers__ only

Start the core stack for Apriltag detections:

    $ dts stack up -H [HOSTNAME] core -d

Make sure the detector is spinning and you get detection messages in `rostopic hz`.

TODO: Could simply check topic name with `rostopic list`. Better put the name here.


### Start the autolab stack

Note: For __all__ robots (Autobot, Watchtower, Duckiehall)

Note: Start with `Duckiehall` robots first

Run the Autolab stack:

    $ dts stack up -H [HOSTNAME] autolab -d


### Check if you get data
Clone the Github repo `duckietown/dt-autolab-localization` and run the following command from the cloned repository directory:

    $ dts devel build -f
    $ dts devel run -L test-tf -- --hostname ETHlargeloop

Note: the separator `--` is not a typo; the hostname is the map name without underscores, so `ETHlargeloop` instead of `ETH_large_loop`. You should see lines like these:

```
watchtower03/camera_optical_frame tag/326
watchtower03/camera_optical_frame tag/307
watchtower03/camera_optical_frame tag/326
watchtower02/camera_optical_frame tag/308
watchtower02/camera_optical_frame tag/322
```

Make sure you get detections from all the watchtowers. Every 10s, the autobots will publish their TF between their footprint and the apriltag on top of them,

```
watchtower04/camera_optical_frame tag/314
autobot01/footprint tag/403
watchtower05/camera_optical_frame tag/301
```

The Duckiehall robot will also publish TF between the map frame and each ground tag (every 10 sec),

```
watchtower02/camera_optical_frame tag/343
world map
map tag/301
map tag/303
map tag/309
map tag/310
map tag/311
map tag/312
map tag/314
map tag/315
map tag/318
map tag/317
map tag/321
map tag/322
map tag/307
map tag/326
map tag/343
watchtower05/camera_optical_frame tag/301
watchtower05/camera_optical_frame tag/307
```

Make sure you get all these types of observations.

### Further data verification (visualized)
Run the command (from the same cloned repo)

    $ dts devel run -f -X -L single-experiment -- --hostname ETHlargeloop

This should wait for 12 seconds for all these observations to come in and put everything in a pose-graph that will be optimized and rendered.


## Integrate Odometry data (wheel encoders)

In order to integrate encoders data into the localization system, you need an extra container that takes the odometry data from the robot and feeds that into the localization system.

NOTE: You need to run this on every Autobot

You can run the odometry integration with the command,

    $ dts stack up -H [HOSTNAME] encoder -d

You can test that the data is correctly received by the localization system by running the test-tf application as we have done above. You should see something like the following, indicating that a transformation between the reference frame `footprint` of the robot at different timestamps is received.

```
autobot01/footprint autobot01/footprint
autobot01/footprint autobot01/footprint
autobot01/footprint autobot01/footprint
```