# installing_arch_mbr
A list of commands which help you to install Arch Linux. Created for ease of access, and also to help other people. Thanks to EFLinux [(@ermanno_ferrari)](https://www.youtube.com/c/EFLinuxMadeSimple) for his videos. 


Connecting to Wifi using `iwctl`:
```
iwctl

(inside iwctl interface)

device list

station [device-name] scan

station [device-name] get-networks

station [device-name] connect <SSID_OF_NETWORK>

(enter password afterwise)
```

Check with `ping google.com` to test internet connection.


For ease of usage, install `openssh` in Arch and then access via your computer.
```
sudo pacman -Sy openssh

sudo systemctl start sshd

ip a

passwd 
(Apply a simple root password here)
```
To login (local PC): `ssh root@ip-address`
(Copy ip address and login as root into the live ISO)

---

The list of commands goes as:
```
timedatectl set-ntp true

fdisk or cfdisk (to create partitions)

mkfs.ext4 /dev/sdXY

mount /dev/sdXY /mnt

pacstrap /mnt base linux linux-firmware nano vim

genfstab -U /mnt >> /mnt/etc/fstab

(To check the output of fstab)
cat /mnt/etc/fstab

arch-chroot /mnt

ln -sf /usr/share/zoneinfo/Asia/Kolkata /etc/localtime

hwclock --systohc

nano /etc/locale.gen
(Here, uncomment the correct locale (en_IN UTF8)

locale-gen

nano /etc/locale.conf
(Here, insert "LANG=en_IN.UTF-8")

nano /etc/hostname
(Enter the desired hostname and save)

nano /etc/hosts
(Here, add these lines:
127.0.0.1 [tab] localhost
::1 [tab x 2] localhost
127.0.1.1 [tab] HCL_C2Duo.localdomain [tab] HCL_C2Duo)

passwd (change root password)

pacman -Sy grub os-prober networkmanager network-manager-applet wpa_supplicant wireless_tools dialog base-devel linux-headers ntfs-3g mtools dosfstools

grub-install --target=i386-pc /dev/sda

grub-mkconfig -o /boot/grub/grub.cfg

exit (from medium)

(In the installer)
umount -a

sudo reboot

(NOW, BOOT INTO THE OS, NOT INSTALLER)
(Login as root, and execute the below ones)

useradd -m -G wheel pranav

passwd pranav
(Set the password)

EDITOR=nano visudo
(Uncomment to allow members of group wheel to execute any command)(with password)

(Save file, and login as Pranav)

sudo systemctl start NetworkManager
sudo systemctl enable NetworkManager

(For wifi: "nmtui")

(Display drivers)
sudo pacman -Sy xf86-video-intel mesa (Intel drivers)
sudo pacman -Sy xf86-video-amd-gpu mesa (AMD)
sudo pacman -Sy xf86-video-vmware (VMWare or VirtualBox)
sudo pacman -Sy nvidia nvidia-utils (Nvidia)
sudo reboot (and again login as Pranav)

sudo pacman -Sy xorg

sudo pacman -Sy gdm

sudo systemctl enable gdm

sudo pacman-Sy gnome gnome-extra 

sudo reboot (and arch is installed!)
```

Note: Most of the steps can be done inside chroot itself; reboot is not very necessary. 
