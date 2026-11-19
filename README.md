# My Hyprland Dotfiles

Personal Linux desktop configuration for Ubuntu, using Hyprland with a Catppuccin theme.

This repository stores my desktop configuration files and helper scripts so I can restore my environment after reinstalling Linux.

## Desktop Overview

| Component | Application |
|---|---|
| Operating System | Ubuntu 24.04 LTS |
| Window Manager | Hyprland |
| Configuration | Lua |
| Wallpaper Manager | Hyprpaper |
| Status Bar | Waybar |
| Application Launcher | Rofi |
| Terminal | Kitty |
| File Manager | Thunar |
| Audio Settings | Pavucontrol |
| Network Settings | NetworkManager Editor |
| Theme | Catppuccin |
| Screenshot | grim + slurp |

GNOME and GDM are retained as the default desktop and login manager.

## Repository Structure

```text
dotfiles/
├── hypr/
│   ├── hyprland.conf
│   ├── hyprland.lua
│   ├── hyprland.lua.bak
│   ├── hyprpaper.conf
│   ├── monitors.conf
│   ├── workspaces.conf
│   └── themes/
│       └── catppuccin-mocha.lua
│
├── waybar/
│   ├── config.jsonc
│   ├── config.jsonc.bak
│   ├── style.css
│   └── themes/
│       └── mocha.css
│
├── rofi/
│   ├── config.rasi
│   ├── catppuccin-default.rasi
│   └── themes/
│       └── catppuccin-mocha.rasi
│
├── kitty/
│   ├── kitty.conf
│   └── mocha.conf
│
├── local-bin/
│   ├── catppuccin-menu
│   ├── catppuccin-switch
│   └── screenshot-tool
│
└── README.md
```

## Features

### Hyprland

- Lua-based configuration.
- Keyboard shortcuts for window management.
- Window floating and maximize controls.
- Workspace navigation.
- Custom startup applications.
- GNOME/GDM remains available.

### Waybar

- Workspace and active-window information.
- Clock and calendar launcher.
- Network status and NetworkManager settings.
- Volume control and Pavucontrol.
- CPU, memory, battery and brightness modules.
- Catppuccin styling.

Mouse actions:

| Module | Left click | Right click |
|---|---|---|
| Network | Open Network Settings | Close Network Settings |
| Volume | Open Pavucontrol | Close Pavucontrol |
| Clock | Open GNOME Calendar | Close GNOME Calendar |

### Wallpaper – Hyprpaper

Hyprpaper handles wallpaper rotation.

Configuration: `hypr/hyprpaper.conf`

- Wallpaper directory: `~/Pictures/Wallpapers`
- Monitor: `eDP-1`
- Fit mode: `cover`
- Rotation interval: 180 seconds
- Order: random

The old Bash slideshow and swaybg-based wallpaper setup have been retired.

### Rofi

- `Super + R`: Application launcher.
- `Super + Shift + R`: Command runner.

### Catppuccin

Supported flavors:

- Latte
- Frappé
- Macchiato
- Mocha

Switch themes using:

```bash
catppuccin-menu
```

Or directly:

```bash
catppuccin-switch mocha
```

### Screenshot Tool

The screenshot helper supports:

- Print: Capture focused monitor.
- Super + Print: Select a region.
- Shift + Print: Capture active window.

Screenshots are saved under:

```text
~/Pictures/Screenshots
```

## Requirements

Install the applications and utilities required by your configuration.

Example Ubuntu package installation:

```bash
sudo apt update

sudo apt install \
    git \
    kitty \
    thunar \
    waybar \
    rofi \
    hyprpaper \
    grim \
    slurp \
    jq \
    wl-clipboard \
    libnotify-bin \
    pavucontrol \
    network-manager-gnome \
    gnome-calendar \
    papirus-icon-theme \
    papirus-folders \
    fcitx5 \
    fcitx5-bamboo
```

Hyprland itself must also be installed and working before restoring its configuration.

Some components, such as Catppuccin GTK themes and Nerd Fonts, may require separate installation.

## Restoring Dotfiles

Clone the repository:

```bash
git clone https://github.com/THT909/Hyperland-dotfile.git ~/dotfiles
```

Back up existing configurations before restoring:

```bash
mkdir -p ~/config-backup

cp -a ~/.config/hypr ~/config-backup/ 2>/dev/null
cp -a ~/.config/waybar ~/config-backup/ 2>/dev/null
cp -a ~/.config/rofi ~/config-backup/ 2>/dev/null
cp -a ~/.config/kitty ~/config-backup/ 2>/dev/null
```

Restore configurations:

```bash
mkdir -p ~/.config

cp -a ~/dotfiles/hypr ~/.config/
cp -a ~/dotfiles/waybar ~/.config/
cp -a ~/dotfiles/rofi ~/.config/
cp -a ~/dotfiles/kitty ~/.config/
```

Restore helper scripts:

```bash
mkdir -p ~/.local/bin

cp -a ~/dotfiles/local-bin/. ~/.local/bin/
chmod +x ~/.local/bin/*
```

Make sure the wallpaper directory exists:

```bash
mkdir -p ~/Pictures/Wallpapers
```

Copy your wallpaper images into that directory separately. Wallpaper images are not stored in this repository.

## After Restoring

1. Verify Hyprland configuration.
2. Verify Hyprpaper configuration and wallpaper directory.
3. Verify Waybar modules and click actions.
4. Verify Rofi keyboard shortcuts.
5. Verify Kitty theme.
6. Verify helper scripts.
7. Test GNOME and GDM remain available.

Reload Hyprland configuration:

```bash
hyprctl reload
```

## Updating Dotfiles

After changing desktop configurations:

```bash
cd ~/dotfiles

git add .
git commit -m "Update desktop configuration"
git push
```

## Notes

- Keep GNOME and GDM working.
- Do not replace GDM with another display manager.
- Do not commit passwords, access tokens or other private information.
- Keep personal wallpaper images backed up separately.
- Review configuration changes before restoring them on another machine.

---

Personal Linux desktop configuration. Built and maintained incrementally.
