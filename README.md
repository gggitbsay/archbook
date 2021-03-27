# archbook

## Old man eyes ...
```
setfont -d

# confirm efi mode
ls /sys/firmware/efi/efivars


# check network & setup time
ip link
ping -c 3 archlinux.org
timedatectl set-ntp true

```

## Backup boot partition

## Partition drive

```
cgdisk /dev/sdx

## Use Linux LVM (8e00) as partition type 
## Should see similar to this

Part. #     Size     Partition Type    Partition Name
-----------------------------------------------------
           3.0 KiB   free space
1        200.0 MiB   EFI System        EFI System Partition
2         372.5 GiB   Apple HFS/HFS+    Macintosh HD
         128.0 MiB   free space
3        93.1 GiB   Linux LVM         ArchLinux
```


## Get off root ... 
https://wiki.archlinux.org/index.php/General_recommendations#Users_and_groups

```
useradd --create-home --groups wheel --shell /bin/bash username
passwd username


https://man.archlinux.org/man/visudo.8
export EDITOR=vim;
visudo
```

Un-comment the wheel group line:
```
%wheel ALL=(ALL) ALL
```

## Exit and start building desktop environment

```
sudo pacman -S xf86-video-intel mesa-libgl libva-intel-driver libva
sudo pacman -S --needed xorg

sudo pacman -S --needed gnome gnome-tweaks

## Touchpad install

sudo pacman -S xf86-input-synaptics


systemctl enable gdm

```
# Gnome crashes immediately after login. Also the mouse pointer appearance is corrupted. 
Let's try installing Intel Microcode. Maybe I should get some lunch first ...

https://wiki.archlinux.org/index.php/Microcode

```
sudo pacman -S intel-ucode

# then edit /boot/loader/entries/<entry>.conf and add this line above the /initramfs-linux.img 
initrd     /intel-ucode.img

```
That didn't fix it, but I now suspect the synaptics driver, or the NVidia driver (I saw some errors scroll by in the console when I tried to read a man page)

```
sudo pacman -R xf86-input-synaptics
```
No such luck. 

Looking at video card issues. 
https://wiki.archlinux.org/index.php/Hardware_video_acceleration
https://mpv.io/manual/stable/#options-hwdec

```
pacman -S mpv








