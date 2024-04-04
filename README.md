## About

DeaDBeeF is a multiple-platform music player for desktop operating systems.

[The Official Website](http://deadbeef.sf.net).

If you wish to chat with developers, join us on [Discord](https://discord.gg/GTVvgSqZrr).

## Download official releases (only GNU/Linux and Windows)

[Downloads Page](https://deadbeef.sourceforge.io/download.html)

## Download nightly (development) builds

<sub><sup>NOTE: The macOS version has not been officially released, and has many unresolved issues and unimplemented features</sup></sub>

[![Linux Build Status](https://github.com/DeaDBeeF-Player/deadbeef/workflows/Build%20for%20Linux/badge.svg)](https://github.com/DeaDBeeF-Player/deadbeef/actions/workflows/linuxbuild.yml)
[![Windows Build Status](https://github.com/DeaDBeeF-Player/deadbeef/workflows/Build%20for%20Windows/badge.svg)](https://github.com/DeaDBeeF-Player/deadbeef/actions/workflows/windowsbuild.yml)
[![macOS Build Status](https://github.com/DeaDBeeF-Player/deadbeef/workflows/Build%20for%20macOS/badge.svg)](https://github.com/DeaDBeeF-Player/deadbeef/actions/workflows/macbuild.yml)

[Nightly GNU/Linux Builds](https://sourceforge.net/projects/deadbeef/files/travis/linux/master/)

[Nightly Windows Builds](https://sourceforge.net/projects/deadbeef/files/travis/windows/master/)

[Nightly macOS Builds](https://sourceforge.net/projects/deadbeef/files/travis/macOS/master/)


## Building DeaDBeeF from source

### Linux, BSD and similar (GTK/*NIX version)

#### Dependencies

The listed package names are for Debian/Ubuntu (tested on Ubuntu 22.04). Package names for your distribution might vary.

* Required build dependencies:
```
apt-get install -y build-essential autoconf automake autopoint libtool clang yasm intltool pkg-config libjansson-dev libblocksruntime-dev libdispatch-dev
```
Note that Debian does not ship `libdispatch0`, so you have to either build or Ubuntu, or get the package from somewhere and install it.

* Optional build dependencies for plugins:
```
apt-get install -y libsamplerate0-dev libgtk-3-dev libasound2-dev libvorbis-dev libcurl4-openssl-dev libjpeg8-dev libpng-dev libmad0-dev libmpg123-dev libflac-dev libwavpack-dev libsndfile1-dev libavformat-dev libpulse-dev libfaad-dev zlib1g-dev libzip-dev libpipewire-0.3-dev libnotify-dev libopusfile-dev libcdio-dev libcddb2-dev libcdio19 
```
If any dependency is missing, then the build is configured without the corresponding plugin. You can see the list of enabled/disabled plugins at the end of `./configure` run.
```
libsamplerate0-dev - for the resampler
libgtk-3-dev - for GTK3 interface
libasound2-dev - for ALSA support
libvorbis-dev - for OGG support
libcurl4-openssl-dev - for Last.fm and vfs_curl support
libjpeg8-dev - for JPEG cover art support
libpng-dev - for PNG cover art support
libmad0-dev - for MP3 support via MAD
libmpg123-dev - for MP3 support via mpg123
libflac-dev - for FLAC support
libwavpack-dev - for Wavpack support
libsndfile1-dev - for wav/aiff support
libavformat-dev - for FFmpeg codecs support
libpulse-dev - for PulseAudio support
libfaad-dev - for AAC support via libFAAD
zlib1g-dev - for psf/psf2/vgz support
libzip-dev - for vfs_zip support
libpipewire-0.3-dev - for Pipewire support
libnotify-dev - for notification popups
libopusfile-dev - for Opus support
libcdio-dev, libcddb2-dev, libcdio19 - for AudioCD support
```
There is also a GTK2 interface that you can use instead of GTK3, but GTK2 has been dropped from Debian/Ubuntu since a long time ago.

#### Building

* Clone the repository (with `--recursive` to also get submodules)
* Remember to get submodules: `git submodule update --init` if you cloned the repository without `--recursive`
* Run `./autogen.sh` to bootstrap
* Run `CC=clang CXX=clang++ ./configure`, optionally with `--disable-<component>` (for the full list of `configure` options, see `./configure --help`, or `INSTALL` file generated by `autogen.sh`)
* Run `make` (optionally with `-j5` for 5 parallel threads)
* Run `sudo make install`

### macOS

* Install Xcode. The latest one is the best, but older versions will usually keep working for a year or two.
* Run `sudo xcode-select --install` - This will configure git and command line build tools
* Clone the deadbeef git repository
* Remember to get submodules: ```git submodule update --init```

#### Command line

* Run ```xcodebuild -project osx/deadbeef.xcodeproj -target DeaDBeeF -configuration Release```
* The output will be located here: ```osx/build/Release/DeaDBeeF.app```

#### Xcode UI

* Open the `osx/deadbeef.xcodeproj` in Xcode, and build/run from there

### Windows

#### Prerequisites

* MSYS2: Install the 64-bit version of [msys2](https://www.msys2.org/) and ensure to run `pacman -Syu`
* Premake5: [v5.0.0-beta1](https://premake.github.io/download)
* Toolchain
```
pacman -S mingw-w64-x86_64-libzip mingw-w64-x86_64-pkg-config mingw-w64-x86_64-dlfcn mingw-w64-x86_64-clang mingw-w64-x86_64-libblocksruntime git make tar xz
```
* Dependencies:
```
pacman -S mingw-w64-x86_64-jansson mingw-w64-x86_64-gtk3 mingw-w64-x86_64-gtk2 mingw-w64-x86_64-mpg123 mingw-w64-x86_64-flac mingw-w64-x86_64-portaudio
```
* Plugin dependencies: follow the [Windows plugin status page ](https://github.com/DeaDBeeF-Player/deadbeef/wiki/Windows-plugin-status) to find out dependencies of the plugins, and install them too.

#### Compiling

* Ensure that you are in mingw64 shell (run mingw64.exe) and clone this git
  repository
* From deadbeef main directory run `premake5 --standard gmake2` using your corresponding path to `premake5.exe`
* Compile with `make config=debug_windows` (debug build) or `make config=release_windows` (stripped/release build)
* Find the resulting binaries in `bin/debug` or `bin/release`

#### Other notes

* GTK3 uses [Windows-10](https://github.com/B00merang-Project/Windows-10) theme and [Windows-10-Icons](https://github.com/B00merang-Artwork/Windows-10) by default. If they are not in msys2 tree, then they must be manually placed in the `share/icons` and `share/themes`. A different theme can be specified by editing the `etc/gtk-3.0/settings.ini` file.

## Licensing

DeaDBeeF core uses ZLIB license. See COPYING in each subdirectory for details.

## Supporting this project

[Please visit the support page](http://deadbeef.sourceforge.net/support.html)
