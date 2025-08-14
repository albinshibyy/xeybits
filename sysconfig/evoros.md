## **_EVOROS CONFIG_**
***Endeavour OS Post-Install Config File***

---

## **Package Installation**

### **Core Tools**

```bash
sudo pacman -S --needed htop btop fastfetch vulkan-radeon xdg-desktop-portal-kde flatpak firejail fish
```

### **Development**

```bash
sudo pacman -S --needed go rust zed
```

### **Desktop Apps**

```bash
sudo pacman -S --needed ollama syncthing kamoso p7zip obsidian virtualbox timeshift
```

### **lts kernal**

```bash
sudo pacman -S --needed linux-headers linux-lts linux-lts-headers
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

## **Flatpak Apps**

Add Flathub repo:

```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```

Install apps:

```bash
flatpak install flathub org.nickvision.tubeconverter io.github.martchus.syncthingtray   io.mrarm.mcpelauncher it.mijorus.gearlever com.usebottles.bottles com.rtosta.zapzap com.microsoft.Edge org.onlyoffice.desktopeditors org.kde.isoimagewriter
```

---

## **AUR Packages**

Install packages:

```bash
paru -S --needed brave-bin vscodium-bin ani-cli
```

---

## **Mirror Ranking**
Using Reflector (with backup and reliability tweaks):
```bash
sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak
sudo reflector --country 'United States,India,Singapore'   --latest 20 --protocol https --sort score   --save /etc/pacman.d/mirrorlist
```

---
