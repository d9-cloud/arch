```fish
timedatectl set-ntp true

timedatectl set-timezone Asia/Novokuznetsk

reflector --country Russia --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

<br>

```fish
fdisk /dev/nvme0n1

g
ENTER
n
ENTER
ENTER
ENTER
+256MiB
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

```fish
mkfs.fat -F 32 /dev/nvme0n1p1

mkfs.ext4 /dev/nvme0n1p2

mount /dev/nvme0n1p2 /mnt

mkdir -p /mnt/efi

mount /dev/nvme0n1p1 /mnt/efi
```

<br>

```fish
pacstrap -K /mnt base base-devel linux linux-firmware intel-ucode grub efibootmgr networkmanager reflector sudo neovim fish
```

<br>

```fish
genfstab -U /mnt >> /mnt/etc/fstab
```

<br>

```fish
arch-chroot /mnt
```

<br>

```fish
ln -sf /usr/share/zoneinfo/Asia/Novokuznetsk /etc/localtime 

hwclock --systohc
```

<br>

uncomment `ru_RU.UTF-8 UTF-8` and `en_US.UTF-8 UTF-8`

```fish
nvim /etc/locale.gen

locale-gen
```

<br>

`LANG=ru_RU.UTF-8`

```fish
nvim /etc/locale.conf
```

<br>

`FONT=cyr-sun16`

```fish
nvim /etc/vconsole.conf
```

<br>

`arch`

```fish
nvim /etc/hostname

touch /etc/hosts

nvim /etc/hosts
```

```
127.0.0.1 localhost
::1 localhost
127.0.1.1 arch
```

<br> 

```fish
passwd

useradd -mG wheel jack

passwd jack

EDITOR=nvim visudo
```

uncomment `%wheel ALL=(ALL:ALL) ALL`

<br>

```fish
grub-install --target=x86_64-efi --efi-directory=/efi --bootloader-id=Arch

nvim /etc/default/grub
```

`GRUB_TIMEOUT=0`

```fish
grub-mkconfig -o /boot/grub/grub.cfg
```

<br>

```fish
systemctl enable NetworkManager

exit

umount -R /mnt

reboot
```

<br>

```fish
chsh

/usr/bin/fish

fish

set -U fish_greeting ""
```

```fish
sudo timedatectl set-ntp true

sudo systemctl enable --now reflector.timer
```

<br>

```fish
sudo nvim /etc/pacman.conf
```

```fish
Color

ILoveCandy

ParallelDownloads = 10

[multilib]
Include = /etc/pacman.d/mirrorlist
```

```fish
sudo pacman -Syu
```

```fish
sudo pacman -Syu plasma-desktop xsettingsd kde-gtk-config kwalletmanager kwallet-pam sddm sddm-kcm firewalld plasma-pa plasma-nm konsole dolphin ark chromium steam telegram-desktop wl-clipboard libreoffice-fresh-ru spectacle fastfetch imagemagick git fuse2
```

```fish
sudo systemctl enable firewalld

sudo systemctl enable sddm

reboot
```
