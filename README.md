```bash
timedatectl set-ntp true

timedatectl set-timezone Asia/Novosibirsk

reflector --country Russia --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

<br>

```bash
fdisk /dev/nvme0n1

g
ENTER
n
ENTER
ENTER
ENTER
+100M
ENTER
t
ENTER
1
ENTER
n
ENTER
ENTER
ENTER
ENTER
w
ENTER
```

<br>

```bash
mkfs.fat -F 32 /dev/nvme0n1p1

mkfs.ext4 /dev/nvme0n1p2

mount /dev/nvme0n1p2 /mnt

mkdir -p /mnt/efi

mount /dev/nvme0n1p1 /mnt/efi
```

<br>

```bash
pacstrap -K /mnt base base-devel linux linux-firmware intel-ucode grub efibootmgr networkmanager reflector sudo nano fish
```

<br>

```bash
genfstab -U /mnt >> /mnt/etc/fstab
```

<br>

```bash
arch-chroot /mnt
```

<br>

```bash
ln -sf /usr/share/zoneinfo/Asia/Novosibirsk /etc/localtime

hwclock --systohc
```

<br>

uncomment `en_US.UTF-8 UTF-8` and `ru_RU.UTF-8 UTF-8`

```bash
nano /etc/locale.gen

locale-gen
```

<br>

`LANG=ru_RU.UTF-8`

```bash
touch /etc/locale.conf

nano /etc/locale.conf
```

<br>

`KEYMAP=en`

```bash
touch /etc/vconsole.conf

nano /etc/vconsole.conf
```

<br>

`arch`

```bash
touch /etc/hostname

nano /etc/hostname

touch /etc/hosts

nano /etc/hosts
```

```
127.0.0.1 localhost
::1 localhost
127.0.1.1 arch
```

<br> 

```bash
passwd

useradd -mG wheel jack

passwd jack

EDITOR=nano visudo
```

uncomment the two lines after "`root ALL=(ALL:ALL) ALL`"

<br>

```bash
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=arch

nano /etc/default/grub
```

`GRUB_TIMEOUT=0`

<br>

```bash
grub-mkconfig -o /boot/grub/grub.cfg
```

<br>

```bash
systemctl enable NetworkManager

exit

umount -R /mnt

reboot
```

<br>

```bash
chsh

/usr/bin/fish

fish

set -U fish_greeting ""
```

<br>

```bash
sudo timedatectl set-ntp true

sudo systemctl enable --now reflector.timer
```

<br>

```bash
sudo nano /etc/pacman.conf
```

```bash
Color

ILoveCandy

ParallelDownloads = 10

uncomment:

[multilib]
Include = /etc/pacman.d/mirrorlist

sudo pacman -Syu
```

<br>

```bash
sudo pacman -Syu plasma-desktop xsettingsd kde-gtk-config kwalletmanager kwallet-pam sddm sddm-kcm firewalld konsole dolphin ark plasma-pa plasma-nm chromium steam telegram-desktop libreoffice-fresh-ru spectacle fastfetch kate git imagemagick fuse2
```

<br>

```bash
sudo systemctl enable firewalld.service

sudo systemctl enable sddm.service

reboot
```
