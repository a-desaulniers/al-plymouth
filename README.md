<h1 align="center">(Arch Linux) al-plymouth</h1>

<p align="center">
My personal Arch Linux plymouth <i>boot sequence</i>, forked from <a href="https://github.com/adi1090x/plymouth-themes">adi1090x.</a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/a-desaulniers/al-plymouth/refs/heads/master/al_preview.gif">
</p>

<br>
</br>

### What is Plymouth?

[Plymouth](http://www.freedesktop.org/wiki/Software/Plymouth) is a project from Fedora and now listed among the [freedesktop.org's official resources](https://www.freedesktop.org/wiki/Software/#graphicsdriverswindowsystemsandsupportinglibraries) providing a flicker-free graphical boot process. It relies on [kernel mode setting](https://wiki.archlinux.org/index.php/Kernel_mode_setting) (KMS) to set the native resolution of the display as early as possible, then provides an eye-candy splash screen leading all the way up to the login manager.

### How do I get plymouth set up?

follow [this](https://wiki.archlinux.org/index.php/plymouth) *archwiki* article to setup plymouth in *archlinux* or any other distro.

### How do I install this this theme?

**Download :** you can download from [releases](https://github.com/a-desaulniers/al-plymouth/releases/download/Final/al-plymouth.zip).

**Clone :** or you can clone this repository if you want - 
```bash
git clone https://github.com/adi1090x/plymouth-themes.git
```

### Important for Arch users

If you're using the AUR package [plymouth](https://aur.archlinux.org/packages/plymouth) or [plymouth-git](https://aur.archlinux.org/packages/plymouth-git), you need to ensure that [cantarell-fonts](https://archlinux.org/packages/extra/any/cantarell-fonts/) or [ttf-dejavu](https://archlinux.org/packages/community/any/ttf-dejavu/) is installed.
Otherwise, the password prompt to unlock a dm-crypt device won't show up.

### How to use these theme?

+ follow the step below (I'm using **archlinux** here)- 
```bash
# packages needed - plymouth, plymouth-x11, plymouth-plugin-script(fedora)

# after downloading or cloning themes, copy the selected theme in plymouth theme dir
sudo cp -r al-plymouth /usr/share/plymouth/themes/

# check if theme exist in dir
sudo plymouth-set-default-theme -l

# now set the theme (al-plymouth, in this case) and rebuilt the initrd
sudo plymouth-set-default-theme -R al-plymouth

# optionally you can test theme by running the script given in repo (plymouth-x11 required)
sudo ./showplymouth.sh 20
```
+ For **debian**(Ubuntu, Kubuntu) based distros-
```bash
# make sure you have the packages for plymouth
sudo apt install plymouth

# after downloading or cloning themes, copy the selected theme in plymouth theme dir
sudo cp -r al-plymouth /usr/share/plymouth/themes/

# install the new theme (al-plymouth, in this case)
sudo update-alternatives --install /usr/share/plymouth/themes/default.plymouth default.plymouth /usr/share/plymouth/themes/al-plymouth/al-plymouth.plymouth 100

# select the theme to apply
sudo update-alternatives --config default.plymouth
#(select the number for installed theme, al-plymouth in this case)

# update initramfs
sudo update-initramfs -u
``` 

### Change distro logo

If you'd like to change the displayed distro logo, copy the logo file to the theme folder (e.g. `/usr/share/plymouth/themes/al-plymouth`) and then add the following content to the theme's `.script` file (e.g. `/usr/share/plymouth/themes/al-plymouth/al-plymouth.script`):

```
# display arch logo
arch_image = Image("arch-logo.png"); # change filename accordingly
arch_sprite = Sprite();

arch_sprite.SetImage(arch_image);
arch_sprite.SetX(Window.GetX() + (Window.GetWidth() / 2 - arch_image.GetWidth() / 2)); # center the image horizontally
arch_sprite.SetY(Window.GetHeight() - arch_image.GetHeight() - 50); # display just above the bottom of the screen
```


### FYI
+ Created and tested on machine with 1366x768 resolution.
+ Yeah, that's how *quarantine* going on :grin:.
+ Stay Home - Stay Safe, Help Fighting CORONA.
