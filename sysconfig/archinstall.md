`Last Updated: 2025-08-10`
`Last Updated Time: 04:55 AM`

---

## **Network Setup**

### **IWCTL (Wi-Fi)**
Enter iwctl:
```bash
iwctl
```
Inside iwctl:
```bash
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect "wifi-name"
```

---

## **Mirror Ranking**
Using Reflector (with backup and reliability tweaks):
```bash
sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
sudo reflector --country 'United States,India,Singapore'   --latest 20 --protocol https --sort score   --save /etc/pacman.d/mirrorlist
```

---

## **Package Installation**

### **Core Tools**
```bash
sudo pacman -S --needed git base-devel fwupd curl rsync wget zip unzip man   power-profiles-daemon net-tools dnsutils amd-ucode htop btop fastfetch   partitionmanager vulkan-radeon linux-headers linux-lts linux-lts-headers xdg-desktop-portal-kde   flatpak firewalld firejail fish kwalletmanager kdeconnect kcalc filelight
```

### **Development**
```bash
sudo pacman -S --needed go rust zed
```

### **Desktop Apps**
```bash
sudo pacman -S --needed ollama okular syncthing kamoso gwenview p7zip unrar obsidian   virtualbox chromium vlc telegram-desktop timeshift
```

---

## **Pacman Configuration**
Edit `/etc/pacman.conf` and enable:
```
Color
ILoveCandy
ParallelDownloads = 5
VerbosePkgLists
```

---

## **Setup AUR (paru)**
```bash
sudo pacman -S --needed base-devel
git clone https://aur.archlinux.org/paru.git
cd paru
makepkg -si
```

---

## **Firewalld Setup**
```bash
sudo pacman -S --needed firewalld plasma-firewall
sudo systemctl enable --now firewalld
sudo firewall-cmd --set-default-zone=public
sudo firewall-cmd --permanent --add-service=dhcpv6-client
sudo firewall-cmd --reload
```
Enable KDE Plasma applet for firewall management.

---

## **Flatpak Apps**
Add Flathub repo:
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
Install apps:
```bash
flatpak install flathub org.nickvision.tubeconverter io.github.martchus.syncthingtray   io.mrarm.mcpelauncher com.github.gabutakut.gabutdm it.mijorus.gearlever com.usebottles.bottles   com.rtosta.zapzap com.microsoft.Edge org.onlyoffice.desktopeditors org.kde.isoimagewriter
```

---

## **AUR Packages**
Install packages:
```bash
paru -S --needed brave-bin vscodium-bin ani-cli
```

---

## **Firmware Updates**
```bash
sudo pacman -S --needed fwupd
sudo fwupdmgr get-devices
sudo fwupdmgr refresh
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

---

## **Bootloader (systemd-boot)**
```bash
sudo bootctl update
bootctl list
sudo mkinitcpio -P
```

---

## **Backup Configs**
```bash
pacman -Qqe > pkglist.txt
sudo tar czf etc-backup.tar.gz /etc
```

---

---

## **Edit system.conf (Boot Optimizations)**
Before making changes, ensure you back up the original configuration:
```bash
sudo cp /etc/systemd/system.conf /etc/systemd/system.conf.bak
```

Edit `/etc/systemd/system.conf` and set:
```ini
[Manager]
DefaultTimeoutStartSec=10s
DefaultTimeoutStopSec=10s
DefaultTasksMax=75%
DefaultCPUAccounting=yes
```

Reload systemd to apply changes:
```bash
sudo systemctl daemon-reexec
```

---

---

## **Bootloader & Kernel Phase Optimizations**

### **Reduce Loader Delay**
Edit systemd-boot configuration to reduce menu timeout:
```bash
sudo nano /boot/loader/loader.conf
```
Set:
```
timeout 1
```
(or `0` for instant boot into the default entry).

### **Reduce Kernel Initialization Delay**
Rebuild initramfs to only include needed modules:
```bash
sudo nano /etc/mkinitcpio.conf
```
In `MODULES=()` add your GPU driver:
```ini
MODULES=(amdgpu)
```
Then rebuild the initramfs:
```bash
sudo mkinitcpio -P
```
This preloads the AMD GPU driver early, reducing kernel startup time.
