# Autolab map {#autolab-map-editor status=draft}


<div class='requirements' markdown="1">

Requires: Knowledge about what a Autolab is [](#part:autolab-definition)

Results: generated map for duckietown
</div>

## Map editor

You can launch the map editor, using command:

    laptop $ dts map editor

You will see:

<div figure-id="fig:editor1" figure-caption="Map editor">
  <img src="images/simple_editor.png" style='width: 25em; height:auto'/>
</div>

## How to create a new map?

You should specify sizes(width, height) of the map and the size of tiles. Default tile size: **0.585**
<div figure-id="fig:editor2" figure-caption="How to create new map">
  <img src="images/create_map.png" style='width: 25em; height:auto'/>
</div>

Then the map generation process should be initialized. Sample editor window:

<div figure-id="fig:editor3" figure-caption="new map">
  <img src="images/result_of_creation_map.png" style='width: 25em; height:auto'/>
</div>

## How to add an object to the map
 
You can add any object(s) from left menu except the first two blocks, "Road tiles" and "Fill tiles", which describe the types of tiles.
For adding an object, you should double click the object in the left menu.
<div figure-id="fig:editor3" figure-caption="add object to map">
  <img src="images/add_stop.png" style='width: 25em; height:auto'/>
</div>

For editing attributes of an object you should do right click of the object and edit its attributes in the opened window. The window should look like:
<div figure-id="fig:editor4" figure-caption="change attribute of obj">
  <img src="images/edit_attr.png" style='width: 25em; height:auto'/>
</div>

For editing tiles, you should activate the brush mode (see Fig.5). After that, you should choose the type of tiles in left menu. Then, one could select/brush the grids to apply the selected tile type.
<div figure-id="fig:editor5" figure-caption="change tile">
  <img src="images/change_tile.png" style='width: 25em; height:auto'/>
</div>

<div figure-id="fig:editor6" figure-caption="example of map">
  <img src="images/tile_road_ex.png" style='width: 25em; height:auto'/>
</div>

<div figure-id="fig:editor7" figure-caption="choose tiles">
  <img src="images/selection_tiles.png" style='width: 25em; height:auto'/>
</div>

## Rotate tiles
For rotation you should select required tiles and click the rotation button in the tool bar (Fig. 8). See Fig. 9 for the illustrated outcome.
<div figure-id="fig:editor8" figure-caption="rotate tiles">
  <img src="images/rotate_tiles.png" style='width: 25em; height:auto'/>
</div>

<div figure-id="fig:editor9" figure-caption="rotate tiles">
  <img src="images/result_rotate.png" style='width: 25em; height:auto'/>
</div>
