# Autobot {#autolab-2-autobots status=draft}

<div class='requirements' markdown="1">

Requires: A [Duckiebot](+opmanual_duckiebot#book) in DB21M or DB19 configuration

Results: An Autobot ready for the localization system and AIDO evaluations

</div>

In this section, the user will modify a standard Duckiebot for Autolab operations.

Note: The term `tag(s)` refers to AprilTag(s).

## Reflash SD cards for unified naming

If the Duckiebot is calibrated, back up the camera and kinematics calibration files.

Use these conventional Autobot hostnames to flash the SD card:

* autobot`XX` (where `[XX]` are fixed 2 digits starting from `01`)

Restore the calibration files (if applicable). 

## Hardware modification

An AprilTag will be mounted on top of the Autobot for localization.

* Download the [AprilTags for Autobots](https://github.com/duckietown/docs-resources_autolab/blob/daffy/AprilTags/Apriltags_autobots.pdf) file, select the range of tags needed (corresponding to the hostnames setup when flashing SD cards) and print the relevant pages.
* Along the ruler lines on edges of the pages, cut out each tag.
* Apply configuration-wise changes and alignment, fix the tag in place.

### DB21M

<div figure-id="fig:db21m">
<img src="opmanual_autolab/images/autobots_db21m.jpg" style="width: 60%"/>
<figcaption>
DB21M Autobot
</figcaption>
</div>

As shown, align the top of the tag with the bottom of fan screws, trim the dangling white paper.

### DB19

Prepare the materials:

* 4 standoffs M3 x 50mm for example from [here](https://www.distrelec.ch/en/spacer-bolt-6mm-50-mm-no-brand-distin3060pa-50/p/14843056?queryFromSuggest=true)
* 8 screws M3 * 8mm
* laser cut [top plate](https://github.com/duckietown/docs-resources_autolab/tree/daffy/Topplate_AprilTag)

<div figure-id="fig:db19-materials">
<img src="opmanual_autolab/images/autobots_db19-materials.jpg" style="width: 80%"/>
<figcaption>
Material needed for modifying DB19
</figcaption>
</div>

Place the tag in the slot on the top plate:

<div figure-id="fig:db19-at-placement">
<img src="opmanual_autolab/images/autobots_db19-at-placement.jpg" style="width: 80%"/>
<figcaption>
Placement of tag
</figcaption>
</div>

Install the standoffs as shown:

<div figure-id="fig:db19-apriltag">
<img src="opmanual_autolab/images/autobots_db19.jpg" style="width: 80%"/>
<figcaption>
DB19 Autobot
</figcaption>
</div>

## Software setup

This setup is the same for all hardware configurations.

### Navigate to the Autobot dashboard, login

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

The "Tag id" field requires 3 digit integers, e.g. `403`. With the provided AprilTags, the "Tag id"s correspond with Autobot hostnames in the following way:

* autobot01 - Tag id 400
* autobot02 - Tag id 401
* autobot03 - Tag id 402
* ...

Click "Save and Apply" and refresh the page. The user inputs should appear in the fields now.

### (Info) Where do the configs go? 

The steps update the configurations in `/data/config/autolab/tag_id` and `/data/config/autolab/map_name` files on the Autobot, which are later used. (So it's equivalent if one `ssh` and change the files directly on the Autobot.)
