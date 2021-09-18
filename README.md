# vscode-retroarch-wiiu

This repository contains the configuration for a VSCode devcontainer, a feature of VSCode
that allows you to leverage a Docker container as a development environment.

This configuration does the following:
- starts from a standardized Ubuntu bionic image provided by Microsoft
- add the specific version of devkitpro needed by RetroArch
- install C/C++ vscode extensions
- configure IntelliSense for the cross-compiler

## Installation

* If you haven't already done so, you will need to [do some initial setup](https://code.visualstudio.com/docs/remote/create-dev-container#_alternative-repository-configuration-folders) within VScode. 
* You also will need Docker Desktop installed (Windows/Mac), or have a working docker daemon set up (Linux).

Once you have configured the Repository Configuration Paths setting, do the following:

1. Clone this repository
2. Under the folder you select for the Repository Configuration Paths setting, create
   a folder structure that mirrors the RetroArch repo you will be working from.

   Example: if your github username is 'example' and you fork `libretro/RetroArch' to your account,
   the folder structure will look like:

   ```
     github.com/
         example/
             RetroArch/
   ```
3. Move the `.devcontainer` folder from this repo into the `RetroArch` directory you created in
   step 2.
4. Verify your repository was cloned via HTTPS: `git remote get-url origin`

   This is important because VSCode needs the get-url to be a URL in order to match it with the
   devcontainer successfully
5. Open RetroArch in VSCode

If you did everything correctly, VSCode should automatically build and launch the container and you'll
see "Dev Container: wiiu-build-container" in the bottom-left corner of the vscode window.

## First Launch

The last step, once you have successfully booted the container, is to change the IntelliSense configuration.

1. Press F1 to open the command palette
2. Run the "C/C++: Select a Configuration..." command
3. Select "WiiU" from the list.

This will ensure IntelliSense is able to successfully find the right system headers.

## Building the wiiu target

1. Copy the *.a file from the core you want to build into the RetroArch directory and 
   rename it to `libretro_wiiu.a`
1. Open a terminal via Terminal > New Terminal
2. Run `make -f Makefile.wiiu`
3. (optional) rename the resulting RPX file (libretro_wiiu.rpx)

The container also has wiiload installed.

```
WIILOAD=tcp:<your wiiu IP address> libretro_wiiu.rpx
```
