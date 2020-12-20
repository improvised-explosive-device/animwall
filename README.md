# animwall-wpgtk

An orchestrator using xwinwrap and mpv to launch animated/gif desktop wallpapers.

This fork adds support for simultanously generating and applying wpgtk themes,
some arguments, and allows automatically pausing the video when the desktop is inactive.
(The latter is hacky for the time being, and will be revised.)

## Dependencies

Required: *xwinwrap, mpv, nice*

Theming: *wpgtk, pywalfox*

Auto-pause: *wmctrl, socat*

## What is this for

For fun.

## Usage

```
$ animwall [ --<arg> -f <path> -p -w ]
 --<arg>    - Pass args beginning with "--" to mpv, ex. "--scale=nearest".
 -f <path>  - Load wallpaper from file instead of animwall.conf.
 -p         - Pause mpv when the desktop is inactive.
 -w         - Generate & apply wpgtk theme from first frame.
 -h         - You are here.
```

Ok, fine it's not that simple.
You'll need a conf file, located at `XDG_CONFIG_HOME/animwall.conf` to properly
run the script. The script will create an example file in the proper format for
you on first run if you do not already have a conf file.

The format of the file is as follows:
```/path/to/wallpaper:WxH+X+Y```

The path and monitor geometry are separated by a `:`. Each pair will be parsed
by the script as a `configuration` and it will output the animated wallpaper
found at `path` to the monitor geometry described by `WxH+X+Y`. The monitor
geometry syntax is enforced by `xwinwrap`.

Multiple `configurations` can be specified in the same file, separated by some
whitespace. A whitespace inside of a `configuration` section will not be parsed
correctly!

By default, `animwall` runs with `nice 19` making it the lowest priority to
reduce resource usage. If you find mpv is not fast enough at nice 19, you can
edit the script to lower this number. It may increase CPU usage.

This script is dumb. ~~It will not auto stop when a window covers the wallpaper
or anything fancy like that.~~ Hacky auto pause function included.

## License

GPLv2

```
  The GPLv2 License

    Copyright (C) 2020  Peter Kenji Yamanaka

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
```
