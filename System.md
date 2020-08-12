```
             /////////////                mirko@rog 
         /////////////////////            --------- 
      ///////*767////////////////         OS: Pop!_OS 20.04 LTS x86_64 
    //////7676767676*//////////////       Host: Zephyrus G GU502DU_GA502DU 1.0 
   /////76767//7676767//////////////      Kernel: 5.4.0-7634-generic 
  /////767676///*76767///////////////     Uptime: 1 min 
 ///////767676///76767.///7676*///////    Packages: 1853 (dpkg), 18 (flatpak) 
/////////767676//76767///767676////////   Shell: zsh 5.8 
//////////76767676767////76767/////////   Resolution: 1920x1080 
///////////76767676//////7676//////////   DE: GNOME 
////////////,7676,///////767///////////   WM: Mutter 
/////////////*7676///////76////////////   WM Theme: Pop 
///////////////7676////////////////////   Theme: Pop [GTK2/3] 
 ///////////////7676///767////////////    Icons: Pop [GTK2/3] 
  //////////////////////'////////////     Terminal: gnome-terminal 
   //////.7676767676767676767,//////      CPU: AMD Ryzen 7 3750H with Radeon Ve 
    /////767676767676767676767/////       GPU: AMD ATI 05:00.0 Picasso 
      ///////////////////////////         GPU: NVIDIA GeForce GTX 1660 Ti Mobil 
         /////////////////////            Memory: 2332MiB / 15883MiB 
             /////////////
```

# Partitions
I have 1 SSD NVMe in my current setup:

- /dev/nvme0n1: 476,96 GiB

## Partition scheme
```
Device            Start       End   Sectors   Size Type
/dev/nvme0n1p1      4096    1023998   1019903   498M EFI System
/dev/nvme0n1p2   1024000    9412606   8388607     4G Microsoft basic data
/dev/nvme0n1p3   9412608  991822510 982409903 472,5G Linux filesystem
```

## rtl8821ce Network controller
Out of the box, Wi-Fi doesn't work. We need to install dkms for `rtl8821ce` network controller.

First of all download/clone the [tomaspinho/rtl8821ce](https://github.com/tomaspinho/rtl8821ce) repository, then install essential packages:
```
sudo apt install bc module-assistant build-essential dkms
```
and run `dkms-install.sh` script from inside the cloned repository:
```
sudo m-a prepare
sudo ./dkms-install.sh
```
and reboot.

## Nvidia flickering
Sometimes after a reboot or suspend, the screen shows a flickering. We need to enable `modeset` to fix the problem:
```
sudo echo "options nvidia-drm modeset=1" > /etc/modprobe.d/nvidia-drm-nomodeset.conf
```

## rog-core
Mine is a Rog laptop, in order to get the keyboard lighting, function buttons and fan modes to work, you need to install [flukejones/rog-core](https://github.com/flukejones/rog-core):
```
sudo add-apt-repository ppa:lukedjones/rog-core
sudo apt-get update
sudo apt-get install rog-core
systemctl daemon-reload && systemctl restart rog-core
```
So let's give the keyboard some light:
```
rog-core -b med
```

Fan mode can be switch with `-f` option:
```
rog-core -f <silent, normal, boost>
```