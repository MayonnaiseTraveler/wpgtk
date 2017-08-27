
# wpgtk

A universal theming software for all themes 
defined in text files, compatible with all terminals, 
with default themes for GTK2, GTK+, openbox and Tint2, that uses 
[pywal](https://github.com/dylanaraps/pywal) as it's core.

you can choose to interact with it in two ways, manage your themes 
from either a cli application or using a GUI.

#### [GUI](https://gfycat.com/DefinitiveSpiffyJohndory)

#### [Powerful command line interface](https://gfycat.com/NeighboringSarcasticEquine)


![interface_image](http://i.imgur.com/aWgqJPG.png)



## Getting Started

### Dependencies

* feh, or any other wallpaper setting software
* python-gobject
* python-imaging
* Pillow (python)
* xsltproc
* pywal

**_Attention:_** If you're using another terminal, you can load the colors on terminal startup
by running `(wpg -t &)` in your terminal.  
You can add this to your terminal's settings, your shell `rc` file or anywhere else 
that allows you to run commands on startup.

# Installing

**_Warning:_** If you have a previous version of wpgtk installed
please delete the contents of your current `~/.wallpapers` as 
they may conflict with the new folder structure (for versions < 4.0 upgrading).

You can install via pip (as root):

```c
# pip3 install wpgtk
```

or install the `wpgtk-git` package via the AUR.  

You can install color-adaptable themes with an included script,
after you install `wpg` you can run `wpg-install.sh`:

```
  Options:
  -h|help       Display this message
  -v|version    Display script version
  -o|openbox    Install openbox themes
  -t|tint2      Install tint2 theme
  -g|gtk        Install gtk theme
  -i|icons      Install icon-set
  ```

This will install all themes:
  ```
$ wpg-install.sh -otgi 
```

And if everything went fine you can now execute `wpg` and it will take
you to the user interface (you will need to install python3-gobject if
you did not install from the AUR).


for more details on the cli interface do:
```
$ wpg -h
```

# Theming

### General Usage

```
usage: wpg [-h] [-s [S [S ...]]] [-r] [-m] [-a [A [A ...]]] [-l]
                   [--version] [-d [D [D ...]]] [-c] [-e [E [E ...]]]
                   [-z [Z [Z ...]]] [-t] [-x] [-y [Y [Y ...]]]

optional arguments:
  -h, --help      show this help message and exit
  -s [S [S ...]]  set the wallpaper and colorscheme, apply changes system-wide
  -r              restore the wallpaper and colorscheme
  -m              pick a random wallpaper and set it
  -a [A [A ...]]  add images to the wallpaper folder and generate colorschemes
  -l              see which wallpapers are available
  --version, -v   print the current version
  -d [D [D ...]]  delete the wallpaper(s) from wallpaper folder
  -c              shows the current wallpaper
  -e [E [E ...]]  auto adjusts the given colorscheme(s)
  -z [Z [Z ...]]  shuffles the given colorscheme(s)
  -t              send color sequences to all terminals
  -x              add, remove and list templates instead of themes
  -y [Y [Y ...]]  add an existent basefile template

```

Files exported when creating a theme are all under the same directory `$HOME/.wallpapers`
this directory contains all exported formats that `pywal` and `wpgtk` have to offer, such
as:

* css variables under `$HOME/.wallpapers/current.css`
* json under `$HOME/.wallpapers/schemes/{image_name}.json`
* xres files under `$HOME/.wallpapers/xres/{image_name}.Xres`
* environment variables under `$HOME/.wallpapers/current.sh` 

### Templates

You can add config files for which `wpgtk` will create a copy and
add a modifiable `template` file to the `~/.themes/color_other` under the file extension `.base`
in which some keywords will be read and replaced in the original with the respective colors
matching those keywords, these keywords are:

```
#COLOR0 #COLORX10
#COLOR1 #COLORX11
#COLOR2 #COLORX12
#COLOR3 #COLORX13
#COLOR4 #COLORX14
#COLOR5 #COLORX15
#COLOR6
#COLOR7
#COLOR8
#COLOR9

#COLORIN (active color)
#COLORACT (inactive color)
```

##### Example
I added a file called `rofi.txt` and wpgtk created a template under `~/.themes/color_other/rofi.sh.base` 
in which I can put keywords that will later be replaced when I change colorschemes with `wpgtk` in the
original file, giving me a dynamic file that changes with my colorscheme.

```
# location: ~/.themes/color_other/rofi.sh.base

color-window "#COLOR0, #COLOR0, #COLOR0"
color-normal "#COLOR0, white, #COLOR0, #COLORACT, white"
color-active "#COLOR0, #COLORACT, #COLOR0, #COLORACT, white"
```

This is the result after applying a colorscheme:

```
# location: ~/Code/scripts/rofi.sh

color-window "#22231D, #22231D, #22231D"
color-normal "#22231D, white, #22231D, #4c837b, white"
color-active "#22231D, #4c837b, #22231D, #4c837b, white"
```

### Configuration

The configuration file should be located at `$HOME/.wallpapers/wpg.conf`
There you can edit settings without the use of the gui.

# Loading at Startup
to load your new wallpaper at startup along with the colors add the following to your 
startup script or simply add it into your startup apps in your DE of choice.

```sh
bash ~/.wallpapers/wp_init.sh
```

# License

This project is licensed under the GPUv2 License - see the [LICENSE](LICENSE) file for details
