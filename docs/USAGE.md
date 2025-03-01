# Usage of wahooMapsCreator <!-- omit in toc -->
- [Usage of wahooMapsCreator](#usage-of-wahoomapscreator)
  - [Always activate environment first](#always-activate-environment-first)
  - [Run wahooMapsCreator for your country](#run-wahoomapscreator-for-your-country)
  - [GUI (Graphical User Interface)](#gui-graphical-user-interface)
  - [CLI (Command Line Interface)](#cli-command-line-interface)
  - [Advanced CLI-Usage](#advanced-cli-usage)
    - [Mandatory CLI arguments](#mandatory-cli-arguments)
    - [Optional arguments](#optional-arguments)
    - [Main arguments](#main-arguments)
    - [Examples](#examples)
  - [POIs - Points of Interest](#pois---points-of-interest)
  - [Contour lines](#contour-lines)
  - [User specific configuration](#user-specific-configuration)

# Usage of wahooMapsCreator
wahooMapsCreator can be used in two different ways:
- as [graphical window](#gui-graphical-user-interface) programm
- as [command line](#cli-command-line-interface) programm

Both ways support the same arguments to be used for the map-creation process. You can choose the arguments via GUI or as [CLI-arguments](#advanced-cli-usage).

## Always activate environment first
```
conda activate gdal-user
```

## Run wahooMapsCreator for your country
It might be a good idea to run wahooMapsCreator first for a small country e.g. Malta to check if everything is running fine.
In a next step you can run it for your own country.

## GUI (Graphical User Interface)

From the `root` folder of wahooMapsCreator, run:
  - `python -m wahoomc gui`

Set your arguments as required via the window:

<img src="./pictures/gui.png" alt="wahooMapsCreator GUI" width=35%>

## CLI (Command Line Interface)

From the `root` folder of wahooMapsCreator, run:
- `python -m wahoomc cli -co <country_name>`

Examples:
- for Malta: `python -m wahoomc cli -co malta`
- for Ireland: `python -m wahoomc cli -co ireland`

## Advanced CLI-Usage
wahooMapsCreator supports many arguments via command line.
For a list of all supported arguments, run:
- `python -m wahoomc cli -h`


wahooMapsCreator provides following arguments, later on, there are some example calls

### Mandatory CLI arguments
One of them is mandatory for running in CLI mode.

| Option | Description                                                                           | Default Value |
| :----- | :------------------------------------------------------------------------------------ | :------------ |
| -co    | One or more Country to create maps or to create maps for. `malta` or `malta,germany`. | -             |
| -xy    | One or more X/Y coordinates to create maps for. `133/35` or `133/35,133/66`.          | -             |


### Optional arguments
If you like to run wahooMapsCreator with another value than the default, use the following arguments.

| Option | Description                                                                                                      | Default Value       |
| :----- | :--------------------------------------------------------------------------------------------------------------- | :------------------ |
| -md    | Maximum age of source maps and other files in days.                                                              | 24                  |
| -nbc   | Do not process border countries of tiles involving more than one country. Only useful when processing a country. | false               |
| -con   | Calculate contour lines (elevation) and integrate into generated maps.                                           | false               |
| -fd    | Force download of files. Download all files new.                                                                 | false               |
| -fp    | Force processing of files. Create all files new.                                                                 | false               |
| -c     | Save uncompressed maps for Cruiser.                                                                              | false               |
| -tag   | File with tags to keep in the output.                                                                            | `tag-wahoo-poi.xml` |
| -z     | Zip the country (and country-maps) folder.                                                                       | false               |
| -v     | Output debug logger messages.                                                                                    | false               |

### Main arguments
**Create maps for a country**
- `python -m wahoomc cli -co <country>`

**Create maps for X/Y coordinates**

In particular for testing adjustments in configuration-files or coding it is helpful to create maps for only one tile or a handful of tiles!

To create maps for only one tile and not a whole country, one can use the X/Y coordinates of that tile. X/Y coordinates can be retrieved from this in zoom-level 8: [link](http://tools.geofabrik.de/map/#8/50.3079/8.8026&type=Geofabrik_Standard&grid=1). 
- `python -m wahoomc cli -xy <xy_coordinate,xy_coordinate>`

### Examples
- for Malta, download new maps if existing maps are older than 100 days and process files even if files exist
  - `python -m wahoomc cli -co malta -md 100 -fp`
- for Germany, download and process whole tiles which involves other countries than the given
  - `python -m wahoomc cli -co germany -bc`
- to create maps for only one tile
  - `python -m wahoomc cli -xy 134/88`
- for multiple tiles
  - `python -m wahoomc cli -xy 134/88,133/88`

## POIs - Points of Interest
For creating maps which include POIs and have them displayed on your Wahoo device, these steps need to be done:
1. Create custom maps including POIs like [normally](#run-wahoomapscreator-for-your-country), POI's are included per default.

Actually, wahooMapsCreator includes fuel stations, backeries, cafes and railway stations POI's into the generated maps. 

2. Copy POIs relevant files to your device
- [:floppy_disk: docu](COPY_TO_WAHOO.md#copy-relevant-files-for-pois)

3. Activate VTM rendering if needed
- [see here](COPY_TO_WAHOO.md#activate-vtm-rendering)
- see also: https://github.com/treee111/wahooMapsCreator/wiki/Enable-hidden-features

## Contour lines
For creating maps which include contour lines and have them displayed on your Wahoo device, these steps need to be done:
1. Enhance your Anaconda environment using [these steps](./QUICKSTART_ANACONDA.md#additions-for--generating-contour-lines)
2. Create custom maps with the argument `-con` like [normally](#run-wahoomapscreator-for-your-country). You will be asked for username/password on first run generating contour lines.
3. Use a theme that renders contour lines

## User specific configuration
You can control popular configuration with your own files in the home directory `wahooMapsCreatorData/_config`.

Actually, it is possible to control which OSM tags will stay on the map while filtering tags ([documentation](TAGS_ON_MAP_AND_DEVICE.md#file-tags-to-keepjson)) with `~/wahooMapsCreatorData/_config/tags-to-keep.json` . Furthermore, you can control which and how OSM tags will be included in the generated maps with tag-wahoo .xml ([documentation](TAGS_ON_MAP_AND_DEVICE.md#file-tag-wahooxml)) in directory `~/wahooMapsCreatorData/_config/tag_wahoo_adjusted/` and specify the file via `-tag` argument or via GUI.

You can start the tool with `python -m wahoomc.init` to copy the files from the python module to the user directory. You'll have a structure and can change the files to your needs.

The tool searches for configuration in your home directory first and secondly (fallback) in the python installation. If a file is in both directories with the same name, the file of the user directory will be used.

The structure of `~/wahooMapsCreatorData/_config/tag_wahoo_adjusted/` is analogue to the one in the repo: `wahooMapsCreatorwahoomc/resources`.
