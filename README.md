# 安裝 debian 使用 debootstrap

## 硬碟分割
自行配置
... 以下略過

## 掛載
```
sudo mount /dev/sda2 /mnt
sudo mount /dev/sda1 /mnt/boot

```

## 安裝基礎
```
sudo debootstrap --arch amd64 testing /mnt https://deb.debian.org/debian/
```

## 掛載其它
```
sudo mount -t proc /proc /mnt/proc/
sudo mount -t sysfs /sys /mnt/sys/
sudo mount -o bind /dev /mnt/dev/
```

## chroot 到 /mnt
```
sudo chroot /mnt /bin/bash
```

## chroot in
```
source /etc/profile
export PS1="(chroot) ${PS1}"
```

## 裝個強大的 vim
```
apt install -y vim
```

## 編輯 fstab
```
cp host /etc/fstab to /mnt/etc/fstab
or create new one
```

## 編輯 source.list
```
cp host /etc/apt/sources.list to /mnt/etc/apt/sources.list
or create new one
```

## update
```
apt-get update
```

## 選擇 timezone
```
dpkg-reconfigure tzdata
or 
 ln -sf /usr/share/zoneinfo/Asia/Taipei /etc/localtime

hwclock --systohc --localtime
```

## 設定 locales
```
apt-get install -y locales

vim /etc/locale.gen

locale-gen
```

## 編輯 resolv.conf
```
vim /etc/resolv.conf
```

## 編輯 hostname
```
vim /etc/hostname
or echo walter > /etc/hostname
```

## 編輯 hosts
```
vim /etc/hosts
```

## 安裝 linux image and header
```
apt-cache search linux-image
apt install -y linux-image-xxx-amd64
apt install -y linux-headers-xxx-amd64

apt-cache search firmware-

apt-get -y install firmware-realtek
apt-get install -y firmware-misc-nonfree
```

## 安裝 Grub Boot loader
```
apt-get install -y grub2 efibootmgr os-prober

sudo cp -r /usr/lib/grub/x86_64-efi /mnt/usr/lib/grub/
```

# 安裝 grub (如果是可移除裝置記得加上 removable)
```
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB --removable --recheck
```

## make grub config
```
grub-mkconfig -o /boot/grub/grub.cfg
```

## 設定 root password
```
passwd
```

## 安裝 sudo
```
apt-get install -y sudo
useradd -m -g users -s /bin/bash walter
passwd walter
gpasswd -a walter sudo
gpasswd -a walter users
```

## 編輯 sudoers
```
vim /etc/sudoers
```

## 安裝 driver
```
apt-get install -y firmware-linux firmware-linux-free firmware-linux-nonfree
apt-get install -y xorg
apt-get install -y alsa-utils
apt-get install -y ntfs-3g
apt-get install -y gvfs 
apt-get install -y blueman
apt-get install -y pcscd pcsc-tools
apt-get install -y usbutils
```

## 安裝其它 tool
```
apt-get install -y pciutils
apt-get install -y xbacklight
apt-get install -y squashfs-tools
apt-get install -y wget git
apt-get install -y genisoimage
apt-get install -y net-tools
ln -s /usr/bin/genisoimage /usr/bin/mkisofs
```

## 安裝 NetworkManager
```
apt-get install -y network-manager network-manager-pptp network-manager-gnome network-manager-pptp-gnome
```

## 安裝 kde plasma
```
apt install -y task-kde-desktop
```

## 安裝 fonts
```
apt-get install -y fonts-dejavu fonts-wqy-microhei
```

## 安裝 fctix
```
apt-get install -y fcitx
apt-get install -y fcitx-chewing
apt-get install -y fcitx-table-boshiamy
apt-get install -y fcitx-frontend-gtk2 fcitx-frontend-gtk3 fcitx-ui-classic
```

## 設定 fcitx
```
vim /etc/profile.d/fcitx.sh
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS="@im=fcitx"

or edit ~/.xprofile
GTK_IM_MODULE=fcitx
QT_IM_MODULE=fcitx
XMODIFIERS=@im=fcitx
```

## 安裝 libcurses prel
```
apt install -y libcurses-perl
```

## 安裝 driver
```
apt-get install -y firmware-linux firmware-linux-free firmware-linux-nonfree
```

## 安裝 additional software
```
tasksel install standard
```

## 安裝 常用工具
```
apt-get -y install vim curl git tmux fish zsh
apt-get -y install htop screenfetch
apt-get -y install python3-pip
apt-get -y install nmap
apt-get -y install openssh-server
apt-get -y install cowsay
apt-get -y install cmatrix
apt-get -y install tree
apt-get -y install cmus
apt-get -y install emacs
apt-get -y install plank
apt-get -y install w3m
```

## 完成 install
```
apt-get clean
```

## 退出
```
exit
```

## umount
```
sudo umount /mnt/dev
sudo umount /mnt/proc
sudo umount /mnt/sys

sudo umount /mnt/boot
sudo umount /mnt
```

## 重開機
```
sudo reboot
```

## Enjoy
