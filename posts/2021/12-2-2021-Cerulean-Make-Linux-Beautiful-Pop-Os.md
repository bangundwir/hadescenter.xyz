---
title: Cerulean - Make Linux Beautiful | Pop! OS | BSPWM 🐱‍🚀
date: 2021-12-02
author: Anonymouse
summary: Cerulean - Make Linux Beautiful
tags:
  - Tips
  - Linux



---

# Cerulean

<iframe width="560" height="315" src="https://www.youtube.com/embed/Le_gTAlBNO8?start=1" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Installation Steps (Ubuntu/Pop! OS 20.04)

**NOTE:** This guide uses `~/Downloads` as the default path for cloning repos

1. Update your repositories:

   ```bash
     sudo apt update
   ```

2. Upgrade your system:

   ```bash
     sudo apt upgrade
   ```

3. Install **bspwm**:

   Install required dependencies (vim included):

   ```bash
   sudo apt install build-essential git vim xcb libxcb-util0-dev libxcb-ewmh-dev libxcb-randr0-dev libxcb-icccm4-dev libxcb-keysyms1-dev libxcb-xinerama0-dev libasound2-dev libxcb-xtest0-dev libxcb-shape0-dev
   ```

   Clone the repository:

   ```bash
   cd ~/Downloads
   git clone https://github.com/baskerville/bspwm.git
   ```

   Compile and install bspwm:

   ```bash
   cd bspwm
   make
   sudo make install
   ```

   Copy bspwm configuration files:

   ```bash
   mkdir ~/.config/bspwm
   cp examples/bspwmrc ~/.config/bspwm
   chmod +x ~/.config/bspwm/bspwmrc
   cd ..
   ```

   **OPTIONAL:** Configure bspwmrc to your liking

   ```bash
   vim ~/.config/bspwm/bspwmrc
   ```

4. Install **sxhkd**:

   Clone the repository:

   ```bash
   git clone https://github.com/baskerville/sxhkd.git
   ```

   Compile and install sxhkd:

   ```bash
   cd sxhkd
   make
   sudo make install
   ```

   Copy sxhkd configuration files:

   ```bash
   mkdir ~/.config/sxhkd
   cp ../bspwm/examples/sxhkdrc ~/.config/sxhkd
   cd ..
   ```

   **OPTIONAL:** Configure the keybind in sxhkdrc to your liking:

   ```bash
   vim ~/.config/sxhkd/sxhkdrc
   ```

   ------

   **NOTE:** Make sure the terminal emulator used in the config file is installed as the terminal will be the only way we can interact with bspwm upon startup after a fresh installation

   ------

5. Install Polybar:

   Install required dependencies:

   ```bash
   sudo apt install cmake cmake-data pkg-config python3-sphinx libcairo2-dev libxcb1-dev libxcb-util0-dev libxcb-randr0-dev libxcb-composite0-dev python3-xcbgen xcb-proto libxcb-image0-dev libxcb-ewmh-dev libxcb-icccm4-dev libxcb-xkb-dev libxcb-xrm-dev libxcb-cursor-dev libasound2-dev libpulse-dev libjsoncpp-dev libmpdclient-dev libcurl4-openssl-dev libnl-genl-3-dev libuv1-dev
   ```

   Clone the repository:

   ```bash
   git clone --recursive https://github.com/polybar/polybar
   ```

   Compile and install **Polybar**:

   ```bash
   cd polybar
   mkdir build
   cd build
   cmake ..
   make -j$(nproc)
   sudo make install
   ```

6. Install Picom:

   Install required dependencies:

   ```bash
   sudo apt install meson libxext-dev libxcb1-dev libxcb-damage0-dev libxcb-xfixes0-dev libxcb-shape0-dev libxcb-render-util0-dev libxcb-render0-dev libxcb-randr0-dev libxcb-composite0-dev libxcb-image0-dev libxcb-present-dev libxcb-xinerama0-dev libpixman-1-dev libdbus-1-dev libconfig-dev libgl1-mesa-dev  libpcre2-dev  libevdev-dev uthash-dev libev-dev libx11-xcb-dev libxcb-glx0-dev
   ```

   Clone the repository:

   ```bash
   git clone https://github.com/ibhagwan/picom.git
   ```

   Build (with Ninja):

   ```bash
   cd picom
   
   git submodule update --init --recursive
   meson --buildtype=release . build
   ninja -C build
   ```

   Install **Picom**:

   ```bash
   sudo ninja -C build install
   cd ..
   ```

   ------

   **NOTE:** Default installation path is `/usr/local`, use this to change the install prefix:

   ```bash
   meson configure -Dprefix=<path> build
   ```

   ------

7. Install Rofi:

   Install required dependencies:

   ```bash
   sudo apt install bison flex libstartup-notification0-dev check autotools-dev libpango1.0-dev librsvg2-bin librsvg2-dev libcairo2-dev libglib2.0-dev libxkbcommon-dev libxkbcommon-x11-dev libjpeg-dev
   ```

   Get necessary releases:

   ```bash
   cd ~/Downloads
   wget https://github.com/davatorium/rofi/releases/download/1.5.4/rofi-1.5.4.tar.gz
   
   wget https://github.com/libcheck/check/releases/download/0.15.1/check-0.15.1.tar.gz
   ```

   Build check:

   ```bash
   cd check-0.15.1
   ./configure
   make
   make check
   ```

   Install check:

   ```bash
   sudo make install
   cd ..
   ```

   Build **rofi**:

   ```bash
   cd rofi
   mkdir build && cd build
   ../configure
   make
   ```

   Install **rofi**:

   ```bash
   sudo make install
   ```

   Enable and use **rofi**:

   ```bash
   vim ~/.config/sxhkd/sxhkdrc
   ```

   Change **dmenu** to:

   ```bash
   rofi -modi run,drun,window -show drun -show-icons -sidebar-mode 
   ```

8. Install spotify:

   ```bash
   curl -sS https://download.spotify.com/debian/pubkey_0D811D58.gpg | sudo apt-key add - 
   
   echo "deb http://repository.spotify.com stable non-free" | sudo tee /etc/apt/sources.list.d/spotify.list
   
   sudo apt update && sudo apt install spotify-client
   ```

9. Install spicetify:

   Install **spicetify**:

   ```bash
   curl -fsSL https://raw.githubusercontent.com/khanhas/spicetify-cli/master/install.sh | sh
   
   sudo chmod a+wr /usr/share/spotify
   
   sudo chmod a+wr /usr/share/spotify/Apps -R
   ```

   Launch Spotify using spicetify:

   ```bash
   spicetify
   spicetify backup apply enable-devtool
   spicetify update
   ```

   Theming:

   ```bash
   cd ~/Downloads
   
   git clone https://github.com/morpheusthewhite/spicetify-themes.git
   cd spicetify-themes
   
   cp -r * ~/spicetify-cli/Themes
   
   cd ~/spicetify-cli/Themes/Dribbblish/
   
   cp dribbblish.js ../../Extensions
   
   spicetify config extensions dribbblish.js
   
   spicetify config current_theme Dribbblish color_scheme nord-dark
   
   spicetify config inject_css 1 replace_colors 1 overwrite_assets 1
   
   spicetify apply
   ```

10. Install alacritty:

    Install **alacritty**:

    ```bash
    sudo apt install alacritty
    ```

    Clone the repo:

    ```bash
    cd ~/Downloads
    git clone https://github.com/VaughnValle/blue-sky.git
    ```

    Apply alacritty theme:

    ```bash
    mkdir ~/.config/alacritty
    cp blue-sky/alacritty/alacritty.yml ~/.config/alacritty/
    ```

    ------

    **NOTE:** If you get the `error: GLSL 3.30 is not supported` error, do this:

    ```bash
    vim /usr/share/applications/com.alacritty.Alacritty.desktop
    ```

    and change `Exec=alacritty` to `Exec=bash -c "LIBGL_ALWAYS_SOFTWARE=1 alacritty"`

    ------

11. Apply the desktop wallpaper:

    ```bash
    sudo apt install feh
    echo 'feh --bg-fill $HOME/Downloads/blue-sky/wallpapers/blue3.png' >> ~/.config/bspwm/bspwmrc
    ```

12. Configure polybar:

    ```bash
    mkdir ~/.config/polybar
    cd ~/Downloads/blue-sky/polybar
    cp * -r ~/.config/polybar
    
    echo '~/.config/polybar/./launch.sh' >> ~/.config/bspwm/bspwmrc
    
    cd fonts
    sudo cp * /usr/share/fonts/truetype/
    ```

13. Install Oh My ZSH!:

    ```bash
    sudo apt install zsh
    
    sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)
    ```

14. Install Powerlevel10k:

    ```bash
    git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
    ```

15. Theme vim:

    ```bash
    mkdir -p ~/.vim/colors
    cd ~/Downloads
    cp blue-sky/nord.vim ~/.vim/colors
    
    git clone https://github.com/vim-airline/vim-airline.git
     
    cd vim-airline
    cp * -r ~/.vim
    cd ~/Downloads
    
    git clone https://github.com/vim-airline/vim-airline-themes.git
     
    cd vim-airline-themes
    cp * -r ~/.vim
    echo 'colorscheme nord' >> ~/.vimrc
    echo let g:airline_theme=\'base16\' >> ~/.vimrc
    ```

16. Theme rofi:

    ```bash
    mkdir -p ~/.config/rofi/themes
    
    cp ~/Downloads/blue-sky/nord.rasi ~/.config/rofi/themes
    
    rofi-theme-selector #preview the "nord theme" with Enter and apply it with Alt+a
     
    # modify keybindings
    vim ~/.config/sxhkd/sxhkdrc
    # replace dmenu with rofi -show drun
    ```

17. Install slim and slimlock:

    Installation **slim** and **slimlock**:

    ```bash
    sudo apt install slim libpam0g-dev libxrandr-dev libfreetype6-dev libimlib2-dev libxft-dev
    
    sudo dpkg-reconfigure gdm3 #select slim
    ```

    ------

    **NOTE:** If you get `fatal error: ft2build.h:` do:

    ```bash
    sudo vim /usr/include/X11/Xft/Xft.h
    ```

    Change line **39**: to `#include <freetype2/ft2build.h>" <truncated>` and do:

    ```bash
    sudo cp /usr/include/freetype2/freetype /usr/include
    ```

    Then run:

    ```bash
    sudo make
    sudo make install
    cd ..
    ```

    ------

    Theming:

    ```bash
    cd ~/Downloads/blue-sky
    
    sudo cp slim.conf /etc && sudo cp slimlock.conf /etc
    
    sudo cp default /usr/share/slim/themes
    ```

[1.]: https://github.com/VaughnValle/blue-sky

