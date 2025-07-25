`Last Updated: 07-16-2005`
`Last Updated Time: 12:14 PM`

#### ***IWCTL (wifi)***
***Get Inside iwctl***
`iwctl`
***Inside iwctl***
```
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect "wifi-name"
```

#### ***Install imp apps***
***From Arch Repo Official***
`git base-devel fwupd curl rsync wget zip unzip man net-tools dnsutils amd-ucode go rust htop btop ollama okular syncthing kamoso gwenview p7zip unrar obsidian timeshift fastfetch partitionmanager zed vulkan-radeon virtualbox xdg-desktop-portal-kde chromium vlc flatpak firewalld firejail fish telegram-desktop kwalletmanager kdeconnect kcalc filelight`

#### ***Setup AUR (paru)***
```
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```


#### ***Firewalld***
`sudo pacman -S firewalld`
*Check and install dependencies for firewall-applet.
maybe make it autostart, restart yeah*
`sudo pacman -S plasma-firewall`
`sudo systemctl enable --now firewalld`
`sudo systemctl status firewalld`

*Enable the Applet in KDE Plasma*

#### ***Flatpak apps:***
***From Flathub Repo***
`flatpak install flathub org.nickvision.tubeconverter io.github.martchus.syncthingtray io.mrarm.mcpelauncher com.github.gabutakut.gabutdm it.mijorus.gearlever com.usebottles.bottles com.rtosta.zapzap com.microsoft.Edge org.onlyoffice.desktopeditors org.kde.isoimagewriter`


#### ***Chaotic AUR***
###### **Setup chaotic aur***
`brave-bin vscodium`

#### ***Updating Firmware***
***If an update is there, plug in power***

```
sudo pacman -S fwupd
sudo fwupdmgr get-devices
sudo fwupdmgr refresh
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

#### ***managing systemd-boot***
```
sudo bootctl update
bootctl list
```

#### ***Other***
`sudo mkinitcpio -P`