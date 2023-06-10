## GALLERY
<img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/1.png" width="400" lign="center">  <img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/2.png" width="400" lign="center">

<img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/3.png" width="400" lign="center"> <img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/4.png" width="400" lign="center">

<img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/5.png" width="400" lign="center"> <img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/6.png" width="400" lign="center">

<img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/7.png" width="400" lign="center"> <img src="https://raw.githubusercontent.com/dolg-off/dk_dotfiles/main/screenshot/8.png" width="400" lign="center">

  
## INFO
|DIstro|[ARCH](https://archlinux.org/)|
|:---:|:---:|
|WM|[DK](https://bitbucket.org/natemaia/dk/src/master/)|
|Bar|[Polybar](https://github.com/polybar/polybar)|
|Terminal|[Alacritty](https://github.com/alacritty/alacritty)|
|Shell|[Fish](https://fishshell.com/)|
|Icon|[Catppuccin Icon Theme](https://www.gnome-look.org/p/1715570)|
|GTK3|[Catppuccine GTK Theme](https://www.gnome-look.org/p/1715554/)|
|Fonts|[JetBrainsMono](https://www.jetbrains.com/lp/mono/)|
|Fonts 2|[JetBrainsMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/JetBrainsMono.zip)|
|Picom|[yshui](https://github.com/yshui/picom)|
|FireFox|[Catppuccine Rosewater](https://github.com/catppuccin/firefox/releases/download/old/catppuccin_mocha_rosewater.xpi)|
|Launcher|[dmenu](https://git.suckless.org/dmenu/)|
  
## INSTALL
```bash
cfdisk /dev/sdaX  (make partition for root & efi)
mkfs.fat -F 32 /dev/sdaX1  
mkfs.ext4 /dev/sdaX2  
mount /dev/sdaX2 /mnt  
mkdir /mnt/boot
mount /dev/sdaX1 /mnt/boot  
  
pacstrap /mnt base linux linux-firmware  
genfstab -U /mnt >> /mnt/etc/fstab  
arch-chroot /mnt  
  
pacman -S grub efibootmgr nano sudo dhcpcd os-prober ntfs-3g  

/etc/locale.gen (uncomment en_US.UTF-8 & ru_RU.UTF-8)  
locale-gen  
  
ln -sf /usr/share/zoneinfo/Region/City /etc/localtime  
hwclock --systohc 

mkdir /boot/efi  
mount /dev/sdaX1 /boot/efi  
grub-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot/EFI --removable  
grub-mkconfig -o /boot/grub/grub.cfg  

passwd  
useradd -m -g users -G wheel -s /bin/bash username  
passwd username  
EDITOR=nano visudo user ALL=(ALL) ALL  
  
systemctl enable dhcpcd  
```  

## KEYBOARD  
sudo nano /etc/X11/xorg.conf.d/00-keyboard.conf  
```bash
Section "InputClass"  
    Identifier "system-keyboard"  
    MatchIsKeyboard "on"  
    Option "XkbLayout" "us,ru"  
    Option "XkbModel" "pc105"  
    Option "XkbOptions" "grp:alt_shift_toggle"  
EndSection  
```
  
## DK INSTALL 
```bash
sudo pacman -S xorg xorg-xinit mesa git base-devel sxhkd alacritty  

git clone https://bitbucket.org/natemaia/dk/src/master/
cd master
make 
make install

.xinitrc:
exec dk
    
chmod u+x .config/dk/dkrc
chmod u+x .config/sxhkd/sxhkdrc
``` 

## SOFT 
```bash
sudo pacman -S pulseaudio pavucontrol firefox pinta telegram-desktop lxappearance nitrogen viewnior geany python  thunar polybar awesome-terminal-fonts dmenu flameshot sublime-text picom zathura
``` 
  
## TERMINAL SOFT  
```bash
sudo pacman -S htop links neofetch ranger ueberzug highlight unzip cmus 
```  
  
## FISH  
```bash
sudo pacman -S fish
fish  
curl -sL https://git.io/fisher | source && fisher install jorgebucaran/fisher  
fisher install jorgebucaran/nvm.fish  
fisher install IlanCosman/tide@v5  
chsh -s /usr/bin/fish  
set -U fish_greeting  
  
tide configure - что бы конфигурировать тильды
```  
  
## Autostart DK on login 
```bash
nano ~/.config/fish/config.fish 

# Start X at login
if status is-login
    if test -z "$DISPLAY" -a "$XDG_VTNR" = 1
        exec startx -- -keeptty
    end
end     
```  
  
## Permission
```bash
chmod +x .config/dk/dkrc
chmod +x .config/sxhkd/sxhkdrc
chmod +x .config/polybar/*.sh
chmod +x .config/rofi/scripts/*.sh
chmod +x .config/picom/picom.sh
chmod +x .config/ranger/scope.sh
chmod +x .config/ranger/plugins/ranger_devicons/*

```  
