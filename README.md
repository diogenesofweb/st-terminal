## Dependencies needed to build

Debian

```bash
# sudo apt install git
sudo apt install build-essential libx11-dev libxft-dev
```

OpenSUSE

```bash
# install with YAST
patterns-devel-base-devel_basis libX11-devel libXft-devel
```

## Install

```bash
git clone --depth 1 https://github.com/diogenesofweb/st-terminal.git
cd st
# Debian
sudo make clean install

# OpenSUSE
sudo make CC=gcc clean install
```

Or clone original ST and add patches one by one

```bash
git clone --depth 1 https://git.suckless.org/st
cd st
```

Apply a patch, repeat steps below for each patch (example: scrollback patch)

```bash
git checkout -b dev
wget https://st.suckless.org/patches/scrollback/st-scrollback-20210507-4536f46.diff
patch -p1 < st-scrollback-20210507-4536f46.diff
# if no problems
mv config.def.h config.h
sudo make clean install
# if no errors
git add .
git commit -m '[patch] added'
git checkout master
git merge dev
```

Customize `config.h`

```bash
# change font
static char *font = "Hack Nerd Font:pixelsize=12:antialias=true:autohint=true";

# increase line height, vertcenter patch needed for this to look correctly
static float chscale = 1.1;

# decrease letter spacing
static float cwscale = 0.9;

# increase padding
static int borderpx = 6;

const int boxdraw = 1;
```

Applied patches:

```bash
st-bold-is-not-bright-20190127-3be4cf1.diff
st-boxdraw_v2-0.8.3.diff
st-scrollback-20210507-4536f46.diff
st-scrollback-mouse-20191024-a2c479c.diff
st-vertcenter-20180320-6ac8c8a.diff
st-anysize-0.8.4.diff # for better window tiling
st-gruvbox-material-0.8.2.diff # color theme
```

Adjust the font (family and size) and copy the desktop entry for app launching.

```shell
# first, install nerd font (Hack)

# edit
vi st.desktop

cp st.desktop ~/.local/share/applications/st.desktop
```

---

Terminal will probably crash on emoji.

But it is a good option for using with Neovim if the hardware is too old for Kitty-terminal.
