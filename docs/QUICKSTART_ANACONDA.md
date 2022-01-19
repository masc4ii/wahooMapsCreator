# Quickstart Guide for Anaconda on Windows and macOS <!-- omit in toc -->

#### Table of contents <!-- omit in toc -->
- [Download and Install required programs](#download-and-install-required-programs)
  - [Anaconda](#anaconda)
  - [Windows, macOS, Linux](#windows-macos-linux)
    - [Install Java](#install-java)
  - [macOS, Linux only](#macos-linux-only)
    - [homebrew](#homebrew)
    - [OSM-tools](#osm-tools)
  - [wahooMapsCreator](#wahoomapscreator)
- [Create Anaconda Environment](#create-anaconda-environment)
- [Run wahooMapsCreator](#run-wahoomapscreator)

# Download and Install required programs

## Anaconda
1. Download `Anaconda Individual Edition` for your OS from

https://www.anaconda.com/products/individual


2. Install `Anaconda Individual Edition` with default settings

## Windows, macOS, Linux
<details>
  <summary>The following programs are needed on every OS</summary>

### Install Java
https://www.oracle.com/technetwork/java/javase/downloads
</details>

## macOS, Linux only
<details>
  <summary>The following programs are needed for macOS and Linux</summary>

### homebrew
Install using terminal
https://brew.sh/

### OSM-tools
1. Install **Osmfilter** using homebrew in terminal:
```
brew install osmfilter
```
2. Install **osmium-tool** using homebrew in terminal:
```
brew install osmium-tool
```
3. Download **Osmosis** latest version from Github
```
brew install osmosis
```

4. Install mapsforge-map-writer plugin (Osmosis Plugin)
* Download the [mapsforge-map-writer](https://search.maven.org/search?q=a:mapsforge-map-writer) plugin, click on "file_download" and select "jar-with-dependecies.jar".
* Put the .jar in this directory. Create it when it doesn't exist:
`~/.openstreetmap/osmosis/plugins`
* more information: https://github.com/mapsforge/mapsforge/blob/master/docs/Getting-Started-Map-Writer.md#plugin-installation
</details>

## wahooMapsCreator
Download the latest .zip file from the [Releases](https://github.com/treee111/wahooMapsCreator/releases) page and save the folder on your drive. Extract the folder.

You can also clone the repository to have the latest coding.

# Create Anaconda Environment
1. Open (or change to) the root of the extracted wahooMapsCreator folder in terminal or cmd prompt
2. Create a new Anaconda environment via
```
conda env create --prefix ./envs -f ./conda_env/enduser.yml
```
3. activate Anaconda environment with the command printed out
```
conda activate <PATH_TO_FOLDER>/wahooMapsCreator/envs
```

Additional informations: https://opensourceoptions.com/blog/how-to-install-gdal-with-anaconda/

# Run wahooMapsCreator
Run wahooMapsCreater as described in the [README](../README.md/#Run-wahooMapsCreator)