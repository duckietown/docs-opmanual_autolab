# Map {#autolab-2-map status=draft}

<!-- Excerpt: Creating and managing the map of your Autolab. -->

<div class='requirements' markdown="1">

Requires: The city layout is fixed and ready.

Results: The city layout is transcribed in duckietown-world, to be used for visualization tools, for localization and much more.

</div>

In this section, the user will formalize the Duckietown built to a predefined map format, and integrate the map into the `duckietown/duckietown-world` Github repository. The formalized map is required for subsequent operations, e.g. localization.

Note: The term `venv` used in texts of this document refers to the python3 virtual environment.

## Setting up duckietown-world

### Fork and clone the repository
Fork the repository [duckietown/duckietown-world](https://github.com/duckietown/duckietown-world) ([how-to](https://docs.github.com/en/get-started/quickstart/fork-a-repo)) and clone your fork to the local machine ([how-to](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github/cloning-a-repository)).

Then, replace the `[path/to]` with the path to where the repository is cloned to, and:

    laptop $ cd [path/to]duckietown-world


Install `git-lfs` and pull all lfs files:

    laptop $ sudo apt update -y && sudo apt install -y git-lfs
    laptop $ git-lfs


### Create the venv 

Note: `duckietown-world` currently needs python3.7 or higher. You should verify this before proceeding.

Install and create venv:

    laptop $ sudo apt update -y && sudo apt install -y python3-venv
    laptop $ python3 -m venv duckietown-world-venv
    laptop $ source duckietown-world-venv/bin/activate


Warning: Please don't add the venv files to git commits.

(Later, to get out of the venv, just run `deactivate`)

### Further setup in the venv

    laptop $ python3 -m pip install --upgrade pip
    laptop $ python3 -m pip install -r requirements.txt
    laptop $ python3 setup.py develop --no-deps


Note: in case the last command returns the error 'Permission denied: 'src/duckietown_world_daffy.egg-info/PKG-INFO ', go to the folder ```src/duckietown_world_daffy.egg-info``` and change permission for the folder itself as well as all the files within the folder with ```sudo chmod 777 *```. After doing this, run the last command again

## Create your map

To create a map interactively with the jupyter notebook, with your venv activated, inside the `duckietown-world`repository:

    laptop $ jupyter notebook


Warning: Please open the notebooks with browsers other than Firefox, which has a known bug with visuals of maps. Chrome works fine.

Now, navigate to the `notebooks` directory and click open `30-DuckietownWorld-maps.ipynb`. Go through the steps in order to get familiar with the code functions until the `Creating new maps` section is reached. Once there, you can start creating your own new map. In the section below there're all the tile names and representation to help you.

You can add your map line by line, until satisfied with the result. Once this is done:

* Adjust the tile size parameter. The size is the interior to exterior size (on most tiles it is 0.585 meters).
* Create, in `duckietown-world/src/duckietown_world/data/gd1/maps` directory, a new yaml file for your map (e.g. `ETH_small_loop.yaml`).
* Copy the working map contents that you just created in the juypter notebook to the yaml map file.
* Check that you haves the tiles and the tile-size.


## Create map visualization files

Once `[MAP_NAME]`.yaml file is composed, in the root of duckietown-world, with venv activated, run (without `.yaml`):

    laptop $ dt-world-draw-maps ![MAP_NAME]


This should generate a new folder with your map name in the `out-draw_maps` directory. You can now move this folder to the `visualization/maps/` folder.

    laptop $ mv out-draw_maps/![MAP_NAME] visualization/maps/


## Verification

If you now go back to the notebook and run the line that lists all maps, you should find yours in the list.

## Committing

Warning: again, please do not commit any venv files.

Now that the map is ready, you can commit locally:

* the map yaml file in `duckietown-world/src/duckietown_world/data/gd1/maps` 
* the generated visualization in `visualization/maps/`

Then push the local commit to your forked repository, and create a pull request to the official `duckietown/duckietown-world` repository ([how-to](https://docs.github.com/en/github/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)).

In case the pull request is not reviewed in time, please ask for help in the `#devel-autolab` channel on the Duckietown Slack.