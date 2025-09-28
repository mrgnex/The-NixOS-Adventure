# The-NixOS-Adventure
A repository documenting my journey with NixOS. Hopefully this will grow into a beginner friendly documentation for using NixOS.
Every code block includes code that needs to be run in the terminal. Konsole is the stock terminal when installing NixOS. Open this terminal and run the commands.

# Contents
[What is NixOS?](https://github.com/mrgnex/The-NixOS-Adventure/edit/main/README.md#what-is-nixos)  
[How to install NixOS?](https://github.com/mrgnex/The-NixOS-Adventure/edit/main/README.md#how-to-install-nixos)

## What is NixOS?
NixOS is an immutable and declarative Linux based operating system. This means that the core system cannot be easily changed and is this case is changed through a configuration file containing code which tells the system what to do.  
This provides an easy and reliable way to configure a system but also allows tracking and sharing of the configuration file. The main benefit is that this configuration is seperate from hardware. This means any configuration should work with any system.  
Deployments become a breeze but it also means the configuration can be shared between people and even can be used after reinstalling. It is also very robust since after every change a new snapshot of the system is made.  
In short, the way NixOS works allows for very robust and durable way to run the operating system.  
More in depth explanations can be found [here](https://www.youtube.com/watch?v=9OMDnZWXjn4) or [here](https://www.youtube.com/watch?v=FJVFXsNzYZQ).  

## How to install NixOS?
You can refer to the [official guide](https://nixos.org/manual/nixos/stable/index.html#ch-installation).  
For simplicity here is a step-by-step instruction on how to install NixOS on your desktop:  
1. Download [Ventoy](https://www.ventoy.net/en/download.html)
2. Install Ventoy onto the USB drive of your choice following [the official instructions](https://www.ventoy.net/en/doc_start.html)
3. Download the [NixOS ISO](https://nixos.org/download/)
4. Put the NixOS ISO onto the prepared Ventoy USB drive
5. Reboot the PC and using your motherboards boot menu or the BIOS select the USB to boot from
6. When booting you can either choose the Gnome or KDE desktop environments. This is just for the installation process. When using a Nvidia graphics card and experiencing issues, choose the nomodeset option.
7. The live environment should start and you should be greeted by the NixOS desktop
8. Select and run the installation tool
9. Go through all the settings and choose your favourite desktop environment. Also enable "Allow unfree software"
10. Choose the erase disk option and make sure the correct disk is selected (you can select swap with hibernate)
11. Let the installer finish (it might be stuck at 46%) and reboot!

## After the first boot
### Choose the update channel
There are a [couple update channels](https://discourse.nixos.org/t/differences-between-nix-channels/13998) to choose from.
If you want the highest stability just use the stable releases, this is the stock setting. You will have to manually update to a newer version when it releases.
This is typically composed of the last two numbers of the current year and the month the channel was released, e.g.: nixos-23.11. You can check the [status of the channels](https://status.nixos.org/).
The stable branch is typically updated in may (xx.05) and november (xx.11).
To upgrade to a newer release (xx.xx being the old release numbers and yy.yy the new numbers):
1. ```sudo nix-channel --add https://nixos.org/channels/nixos-yy.yy nixos```
2. ```sudo nix-channel --remove nixos-xx.xx```
3. ```sudo nix-channel --update && sudo nixos-rebuild switch```

The unstable channel is bleeding edge and turns it in a sort of rolling release distribution. Do some research if you want to use this channel!
To select the unstable channel:
1. ```sudo nix-channel --add https://nixos.org/channels/nixos-unstable nixos```
2. ```sudo nix-channel --update && sudo nixos-rebuild switch```

### Enable flakes
Enabling flakes is generally good practice. This can be done quite easily.
1. ```sudo nano /etc/nixos/configuration.nix```
2. Add this line anywhere in the configuration file: ```nix.settings.experimental-features = [ "nix command" "flakes"];```
3. ```cd /etc/nixos```
4. ```nix flake init```
5. ```nix flake update```
