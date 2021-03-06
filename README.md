# regolith-de
Standalone Regolith desktop environment for Arch Linux

This is a PKGBUILD for Regolith Linux's fork of the i3 (plus Gnome-flashback) window manager/desktop environment, to rather hackily rip the desktop environment for Regolith Linux and make it work on Arch Linux and it's derivatives. 

Given that Regolith is based on Ubuntu, this will likely only be updated when new releases come out (20.04, 20.10, etc.), barring of course something breaks. But package versions will be taken from the "Release" branch of the Regolith PPA repo, as opposed to "Stable," "Unstable," or "Experimental." If that changes, it'll be noted in the README.

Where possible (more accurately, where I've found possible), Arch/AUR packages will be used if compatible versions exist. Currently Arch's i3-gaps, rofi, and some other packages are being used. Remontoire is in the AUR as `remontoire-git` and will need to be installed manually when using `makepkg` and not an AUR helper, as `makepkg` will *not* pull in dependencies from the AUR. This is why for the time being, `remontoire` is not listed as a hard dependency. It will likely be added when this goes live on the AUR. 

Because of the way AUR packages work, combined with Ubuntu-specific idiosyncracies in the original config file for Regolith's i3, I've had to bundle the regolith build of st - the simple terminal, and use that as the default terminal. Feel free to change it in the config file (`/etc/regolith/i3/config`) just like you would with regular i3, it's just the only other option was for there to be no default terminal, or else try and choose one that some people will have and others won't. I get around this by just including the terminal, and luckily it's st so it's really small. It's its own package, so you can also remove it (`sudo pacman -R regolith-st`), it's not a dependency of anything, it just gets installed with the meta-package. 

This package conflicts with `gnome-shell`, which means it also (unfortunately) will conflict with GDM. For some reason, `gnome-shell` is a hard dependency of the `gdm` package on Arch, but not Ubuntu. On Ubuntu, the Regolith Desktop Environment actually does conflict with GNOME, but not GDM or the `gnome-shell` package alone. But on Arch, whatever the conflict is, is present in the `gnome-shell` package.

## Contributing

PRs are welcome.

If you would like to test this PKGBUILD, the first steps would be to try it out in a Virtual Machine.

**Virtual Machine**

1. Spin up a new VM with a fresh install of Arch Linux.

2. Install git and download the source code for this repo.

    ```
    $ sudo pacman -Sy git
    
    $ mkdir -p ${HOME}/Downloads/build &&cd $_

    $ git clone https://github.com/gardotd426/regolith-de.git && cd regolith-de
    ```

4. [Install the packages](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_and_upgrading_packages)

    ```
    $ makepkg -si
    ```
5. Install optional dependencies

    Until this PKGBUILD is live it isn't possible to include dependencies from the AUR. These will need to be installed manually while in testing.

    [Install the following from the AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_and_upgrading_packages) :
    - [remontoire-git](https://aur.archlinux.org/packages/remontoire-git/) - For the help overlay

6. Start Regolith Desktop Environment

    One way to do this is to run the session from a manual xorg startup:

    ```
    $ sudo pacman -Sy xorg-xinit

    $ echo 'exec i3-gnome-flashback-session' > ${HOME}/.xinitrc

    $ startx
    ```

Note: VMs generally don't play well with picom/compton compositing. If you have any issues with performance, make sure to kill the compositor.

IF THIS MESSAGE IS STILL PRESENT, IT IS NOT READY FOR PRIMETIME. EITHER DON'T TRY IT AT ALL, OR TRY AT YOUR OWN RISK. THERE IS NO WARRANTY.

When I and anyone else working on this decide that it's ready, we will make it available in the AUR. 

## Credits

Credit to Kevin Gilmer @kgilmer for the creation of Regolith Linux as well as invaluable insight during the creation of this PKGBUILD. 
Pull requests are welcome, the number of packages here is enormous (it is a full desktop environment, after all), and this is my first software/package management project of any kind. 

Much credit also to Avinash Duduskar, for already many contributions. 
