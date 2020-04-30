# Autolab map {#autolab-map-making status=ready}

Excerpt: Creating and managing the map of your Autolab.

<div class='requirements' markdown="1">

Requires: The city layout is fixed and ready.

Results: The city layout is transcribed in duckietown-world, to be used for visualization tools, for localization and much more.

Next Steps: todo
</div>

In the following chapters of the book, there are many uses to a software defined map of your Autolab. It is for instance required for a working localization pipeline.

Warning: this part is in chapter B for structural design of the documentation. However, in [](#autolab-auto-charging) you will probably modify the layout of your city. We strongly recommend to do it first then come back here once the map is fixed (to avoid having to do it again).

## Setting up duckietown-world

### Creating a virtual environment for python3

We recommend that you create a virtual environment for duckietown-world.

Here is one possible method, but you can use whichever you prefer.

Note: duckietown-world currently needs python3.7 or higher.

First, install venv:


    laptop $ sudo apt install -y python3-venv


Then, cd into your `duckietown-world` repository (it should be in the `src` folder of `dt-env-developer`), and create the venv.


    laptop $ cd ~/dt-env-developer/src/duckietown-world
    laptop $ python3.7 -m venv duckietown-world-venv
    laptop $ source duckietown-world-venv/bin/activate

Warning: if you create the venv as suggested inside duckietown-world, be very careful not to add it to your git commits.

To verify the version of Python running inside the virtual environment run:

    laptop $ python --version

This should be 3.7.x or higher.

Note: to get out of the virtual environment, just run `deactivate`

### Pip setup of duckietown-world

Now, you can setup duckietown-world. Inside of the virtual environment (you should see "(duckietown-worl-venv)" in front of your prompt line), please run:

    laptop $ python3 -m pip install --upgrade pip
    laptop $ python3 -m pip install -r requirements.txt
    laptop $ python3 -m pip install jupyter
    laptop $ python3 setup.py develop --no-deps

Note: in case the last command returns the error 'Permission denied: 'src/duckietown_world_daffy.egg-info/PKG-INFO ', then go to the folder ```src/duckietown_world_daffy.egg-info``` and change permission for the folder itself as well as all the files within the folder using ```sudo chmod 777```. After doing this, run again:

    laptop $ python3 setup.py develop --no-deps

## Using duckietown-world to create your map

The best way to create a map is to do it interactively with the notebook.

Still in duckietown-world with your virtual environment, run

    laptop $ jupyter notebook


Warning: Please make sure it opens with some other browser than Firefox, which has a known bug with visuals of maps. Chrome works fine.

Now, navigate to notebooks and open `30-DuckietownWorld-maps`. You can run each step in order to get familiar with the code functions.

Once you get to the `Creating new maps` section, you can happily start creating your map. In the section below it is all the tile names and representation to help you.

You can add your map line by line, until satisfied with the result. Once this is done:

* Adjust the tile size parameter. The size is the interior to exterior size (on most tiles it is 0.585 meters).
* Create, in `duckietown-world/src/duckietown_world/data/gd1/maps`, a new map with your name (eg `autolab-ETHZ-01.yaml`).
* Copy the working map description that you just created in there.
* Check that you haves the tiles and the tile-size.

Now, in the root of duckietown-world, run

    laptop $ dt-world-draw-maps ![NEW_MAP_NAME]

This should generate a new folder name after your map in `out-draw_maps`. You can now move this folder to the `visualization/maps/` folder.


## Verification

If you now go back to the notebook and run the line that lists all maps, you should find yours in the list.

## Committing

Now that the map is ready, you can commit :

* the map in `duckietown-world/src/duckietown_world/data/gd1/maps`
* the generated folder is `visualization/maps/`

Note: You may note have the rights to push to the duckietown repository. Instead, create a fork of the repository and remember the user account you use, as it will be useful later on. Also remember the name you gave to the map.

Warning: again, please do not commit any virtual environment.
