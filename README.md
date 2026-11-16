# My Dotfiles

Personal Linux desktop configuration — Ubuntu 24.04 + Hyprland + Catppuccin.

> A personal backup of my Linux desktop environment.
> Keep this repository updated whenever configurations change.

---

## 1. Desktop Environment

| Component | Software |
|---|---|
| OS | Ubuntu 24.04 LTS |
| Window Manager | Hyprland |
| Display Manager | GDM |
| Desktop Environment | GNOME |
| Terminal | Kitty |
| File Manager | Thunar |
| Status Bar | Waybar |
| Application Launcher | Rofi |
| Wallpaper | swaybg |
| Input Method | Fcitx5 + Bamboo |
| Theme | Catppuccin |
| Icon Theme | Papirus |

**Important:** Keep GDM and GNOME working. Do not replace GDM with another display manager during restoration.

---

## 2. Repository Structure

Expected structure:

```text
dotfiles/
├── README.md
├── hypr/
├── waybar/
├── rofi/
├── kitty/
├── local-bin/
├── wallpapers/
├── packages/
│   └── manual-packages.txt
└── restore.sh
```

Some folders and files may not exist yet. Add them as they are backed up.

---

## 3. Required Packages

### Core desktop

```bash
sudo apt install \
    git \
    kitty \
    thunar \
    rofi \
    waybar \
    swaybg \
    grim \
    slurp \
    jq \
    wl-clipboard \
    libnotify-bin \
    pavucontrol \
    network-manager-gnome \
    brightnessctl \
    gnome-calendar
```

### Input method

```bash
sudo apt install fcitx5
```

Install and configure the Bamboo input method separately if it is not available in the current package repositories.

### Fonts

- JetBrainsMono Nerd Font
- Symbols Nerd Font

Check installed fonts:

```bash
fc-list | grep -Ei 'JetBrains|Nerd'
```

### Hyprland

Install Hyprland using a trusted installation source appropriate for the target Linux distribution.

Check:

```bash
hyprctl version
```

---

## 4. Configuration Backup Checklist

### Hyprland

- [ ] `~/.config/hypr/hyprland.lua`
- [ ] `~/.config/hypr/themes/`
- [ ] Check keybindings
- [ ] Check monitor configuration
- [ ] Check startup commands
- [ ] Check Lua configuration dependencies

### Waybar

- [ ] `~/.config/waybar/config.jsonc`
- [ ] `~/.config/waybar/style.css`
- [ ] `~/.config/waybar/themes/`
- [ ] Check workspace module
- [ ] Check clock
- [ ] Check network
- [ ] Check audio
- [ ] Check brightness
- [ ] Check battery
- [ ] Check CPU and memory
- [ ] Check system tray

### Rofi

- [ ] `~/.config/rofi/`
- [ ] Catppuccin theme
- [ ] Application launcher (`drun`)
- [ ] Command launcher (`run`)
- [ ] Check keyboard shortcuts

### Kitty

- [ ] `~/.config/kitty/`
- [ ] Theme configuration
- [ ] Font configuration
- [ ] Terminal appearance

### Scripts

- [ ] `~/.local/bin/catppuccin-switch`
- [ ] `~/.local/bin/catppuccin-menu`
- [ ] `~/.local/bin/screenshot-tool`
- [ ] `~/.local/bin/wallpaper-slideshow`

Check executable permissions after restoring:

```bash
chmod +x ~/.local/bin/*
```

---

## 5. Catppuccin Theme

Supported flavors:

- Latte
- Frappé
- Macchiato
- Mocha

Accent color: Mauve.

Check:

- [ ] Hyprland colors
- [ ] Waybar colors
- [ ] Rofi colors
- [ ] Kitty colors
- [ ] GTK theme
- [ ] Papirus folder colors
- [ ] Theme switching script

Switch theme:

```bash
catppuccin-switch mocha
```

Replace `mocha` with `latte`, `frappe`, or `macchiato` as needed.

---

## 6. Wallpaper

Wallpaper directory:

```text
~/Pictures/Wallpapers/
```

Check:

- [ ] Wallpaper images backed up
- [ ] Wallpaper slideshow script restored
- [ ] swaybg installed
- [ ] Slideshow starts automatically in Hyprland
- [ ] Wallpaper changes every 180 seconds
- [ ] GNOME wallpaper still works independently

---

## 7. GNOME and GDM

These components should remain functional.

- [ ] GDM starts normally
- [ ] GNOME session works
- [ ] GNOME wallpaper works
- [ ] GTK theme works
- [ ] Icon theme works
- [ ] GNOME Calendar works

Do not replace or disable GDM just to configure Hyprland.

---

## 8. Restore Configuration

Clone the repository:

```bash
git clone YOUR_REPOSITORY_URL ~/dotfiles
```

Back up existing configurations before restoring:

```bash
mkdir -p ~/config-backup

cp -a ~/.config/hypr ~/config-backup/ 2>/dev/null || true
cp -a ~/.config/waybar ~/config-backup/ 2>/dev/null || true
cp -a ~/.config/rofi ~/config-backup/ 2>/dev/null || true
cp -a ~/.config/kitty ~/config-backup/ 2>/dev/null || true
```

Restore configurations:

```bash
cp -a ~/dotfiles/hypr ~/.config/
cp -a ~/dotfiles/waybar ~/.config/
cp -a ~/dotfiles/rofi ~/.config/
cp -a ~/dotfiles/kitty ~/.config/
```

Restore scripts:

```bash
mkdir -p ~/.local/bin
cp -a ~/dotfiles/local-bin/. ~/.local/bin/
chmod +x ~/.local/bin/*
```

Restore wallpapers if backed up:

```bash
mkdir -p ~/Pictures/Wallpapers
cp -a ~/dotfiles/wallpapers/. ~/Pictures/Wallpapers/
```

Review paths before running commands if your repository structure differs.

---

## 9. Post-Installation Verification

### Hyprland

```bash
hyprctl version
hyprctl monitors
hyprctl reload
```

- [ ] Hyprland starts
- [ ] Keyboard shortcuts work
- [ ] Floating works (`SUPER + V`)
- [ ] Fullscreen works (`SUPER + F`)
- [ ] Terminal opens (`SUPER + Q`)
- [ ] File manager opens (`SUPER + E`)

### Waybar

```bash
pgrep -a waybar
```

If Waybar is not running:

```bash
waybar -c ~/.config/waybar/config.jsonc \
       -s ~/.config/waybar/style.css &
```

- [ ] Bar appears
- [ ] Clock works
- [ ] Network works
- [ ] Audio controls work
- [ ] Battery works
- [ ] CPU and memory work
- [ ] Tray works

### Rofi

- [ ] `SUPER + R` opens application launcher
- [ ] `SUPER + SHIFT + R` opens command launcher
- [ ] Catppuccin theme works

### Wallpaper

- [ ] swaybg works
- [ ] Wallpaper loads
- [ ] Slideshow works
- [ ] Automatic startup works

### GNOME

- [ ] GDM login screen works
- [ ] GNOME session starts
- [ ] GNOME settings work

---

## 10. Package Backup

Save manually installed packages:

```bash
apt-mark showmanual > ~/manual-packages.txt
```

Restore package list on Ubuntu:

```bash
sudo apt update
xargs -a ~/manual-packages.txt sudo apt install -y
```

Review the package list before restoring. Some packages may not exist on a newer Ubuntu release.

---

## 11. Git Backup

After changing configurations:

```bash
cd ~/dotfiles

git status
git add .
git commit -m "Update desktop configuration"
git push
```

Before publishing, check for passwords, API tokens, personal information and machine-specific files.

---

## 12. Final Checklist

- [ ] All configuration files backed up
- [ ] All scripts backed up
- [ ] Executable permissions preserved
- [ ] Package list saved
- [ ] Wallpapers backed up
- [ ] Fonts documented
- [ ] GTK and icon themes documented
- [ ] Fcitx5 and Bamboo documented
- [ ] GNOME and GDM verified
- [ ] Restore instructions tested
- [ ] GitHub repository updated

---

**Project:** My Personal Linux Dotfiles  
**Primary system:** Ubuntu 24.04 LTS  
**Window manager:** Hyprland  
**Theme:** Catppuccin Mocha + Mauve

*This README is a living document. Update it whenever the desktop configuration changes.*
