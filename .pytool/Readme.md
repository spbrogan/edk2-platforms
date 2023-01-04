# Edk2-Platforms Continuous Integration

This file focuses on information for those working with the `.pytools` directory
directly or interested in lower-level details about how Core CI works.

## Running CI - Read for context

If you just want to get started building code, visit
[Build Instructions](https://github.com/tianocore/tianocore.github.io/wiki/How-to-Build-With-Stuart)
on the TianoCore wiki.  

__NOTE__: In this prototype the Edk2 repo is managed as a dependency in the CISettings.py file.
There are numerous other options like submodule, ext_dep, manifest, etc.  For now, CI_Setup dependency
are used which means when following the steps defined in the build instructions above instead of calling
`stuart_setup` you must call `stuart_ci_setup`. 

For more details check out the Edk2 Pytool Extensions docs <https://www.tianocore.org/edk2-pytool-extensions/>

## Running CI for Edk2-Platforms prototype using Windows 11, VS2019, python 3.10

Read the docs listed above but here are the specifics for this repo that I have used.

1. `git clone --single-branch --branch enable_ci_v1 https://github.com/spbrogan/edk2-platforms.git`
2. make virtual env and activate it 
3. move to cwd to repo workspace `cd edk2-platforms`
4. install pip-requirements into virtual environment `pip install -r pip-requirements.txt`
5. stuart ci setup to get edk2  `stuart_ci_setup -c .pytool\CISettings.py TOOL_CHAIN_TAG=VS2019`
6. build the basetools from edk2 `python edk2\BaseTools\Edk2ToolsBuild.py -t VS2019`
7. stuart update to get other dependencies `stuart_update -c .pytool\CISettings.py TOOL_CHAIN_TAG=VS2019 -a IA32,X64`
9. stuart ci build to run ci `stuart_ci_build -c .pytool\CISettings.py TOOL_CHAIN_TAG=VS2019 -a IA32,X64`

## Basic Status

| Package             | Windows VS2019 (IA32/X64) | Ubuntu GCC (IA32/X64/ARM/AARCH64) | Known Issues |
|:--------------------|:--------------------------|:----------------------------------|:-------------|
| Ext4Pkg             | :heavy_check_mark:        |                                   |    YES       |
| Usb3DebugFeaturePkg | :heavy_check_mark:        |                                   |    YES       |
