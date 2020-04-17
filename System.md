```
             /////////////                mirko@pop-os 
         /////////////////////            ------------ 
      ///////*767////////////////         OS: Pop!_OS 19.10 x86_64 
    //////7676767676*//////////////       Host: TM1701 
   /////76767//7676767//////////////      Kernel: 5.3.0-7648-generic 
  /////767676///*76767///////////////     Uptime: 9 mins 
 ///////767676///76767.///7676*///////    Packages: 2075 (dpkg) 
/////////767676//76767///767676////////   Shell: zsh 5.7.1 
//////////76767676767////76767/////////   Resolution: 1920x1080 
///////////76767676//////7676//////////   DE: GNOME 3.34.3 
////////////,7676,///////767///////////   WM: GNOME Shell 
/////////////*7676///////76////////////   WM Theme: Pop 
///////////////7676////////////////////   Theme: Pop [GTK2/3] 
 ///////////////7676///767////////////    Icons: Pop [GTK2/3] 
  //////////////////////'////////////     Terminal: gnome-terminal 
   //////.7676767676767676767,//////      CPU: Intel i5-8250U (8) @ 3.400GHz 
    /////767676767676767676767/////       GPU: NVIDIA GeForce MX150 
      ///////////////////////////         GPU: Intel UHD Graphics 620 
         /////////////////////            Memory: 2611MiB / 7845MiB 
             /////////////
                                                                  

```

# Partitions
I have 2 SSDs in my current setup:

- /dev/nvme1n1: 238,49 GiB,
- /dev/nvme0n1: 465,78 GiB

## Partition scheme
```
Device            Start       End   Sectors   Size Type
/dev/nvme0n1p1     2048  16582654  16580607   7.9G Linux swap
/dev/nvme0n1p2 16582656  17811454   1228799   600M EFI System
/dev/nvme0n1p3 17811456 976773119 958961664 457.3G Linux LVM


Device         Start       End   Sectors   Size Type
/dev/nvme1n1p1  2048 500117503 500115456 238.5G Linux LVM
```
I installed the system on an LVM volume so you can use both `nvme0n1p3` and `nvme1n1p1` partitions:
```
  --- Physical volume ---
  PV Name               /dev/nvme0n1p3
  VG Name               MiGroup
  PV Size               <457.27 GiB / not usable 3.00 MiB
  Allocatable           yes (but full)
  PE Size               4.00 MiB
  Total PE              117060
  Free PE               0
  Allocated PE          117060
  PV UUID               9toe3D-LKs0-tQh6-xT3Y-a7bT-yhPe-YbRu4S
   
  --- Physical volume ---
  PV Name               /dev/nvme1n1p1
  VG Name               MiGroup
  PV Size               238.47 GiB / not usable 0   
  Allocatable           yes (but full)
  PE Size               4.00 MiB
  Total PE              61049
  Free PE               0
  Allocated PE          61049
  PV UUID               LuTEIC-fsDY-wwKu-kDmZ-SK3e-ntV3-TrXdBX
```

## Realtek ALC298 Fix
The microphone output was not immediately detected but I solved it by adding the following instruction in path `/etc/modprobe.d/alsa-base.conf`:
```
options snd-hda-intel model=alc298-dell1
```
reboot and it just works.