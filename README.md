# HyprOSD

A fork of SwayOSD with Hyprlang support and additional features.
Heavily WIP (fresh fork)
Obviously huge credits to SwayOSD, and I'll try to keep up with their progress. I just forked to make something that's more integrated with Hyprland.

## Roadmap
- [ ] Hyprlang Conf Support
    - [ ] Styling
      - [ ] Radius 
      - [ ] Background
      - [ ] Border
    - [ ] Display selection
    - [ ] Custom Toggles
## Features:

- LibInput listener Backend for these keys:
  - Caps Lock
  - Num Lock
  - Scroll Lock
- Input and output volume change indicator
- Input and output mute change indicator
- Customizable maximum Volume
- Capslock change (Note: doesn't change the caps lock state)
- Brightness change indicator

## Install:

There's a new LibInput watcher binary shipped with SwayOSD (`swayosd-libinput-backend`)
which can automatically detect key presses, so no need for binding key combos.
The supported keys are listed above in [Features](#features)

### Through Meson

```zsh
# Please note that the command below might require `--prefix /usr` on some systems
meson setup build
ninja -C build
meson install -C build
```

## Usage:

### HyprOSD LibInput Backend

Using Systemd: `sudo systemctl enable --now swayosd-libinput-backend.service`

Other users can run: `pkexec swayosd-libinput-backend`

##### Start Server

```bash
# OSD server
exec-once = swayosd-server
```

##### Add Client bindings

```bash
# Sink volume raise optionally with --device
bind =, XF86AudioRaiseVolume, exec, swayosd-client --output-volume raise
# Sink volume lower optionally with --device
bind =, XF86AudioLowerVolume, exec,  swayosd-client --output-volume lower --device alsa_output.pci-0000_11_00.4.analog-stereo.monitor
# Sink volume toggle mute
bind =, XF86AudioMute, exec, swayosd-client --output-volume mute-toggle

# Brightness raise
bind=, XF86MonBrightnessUp, exec, swayosd-client --brightness raise
# Brightness lower
bind=, XF86MonBrightnessDown, exec, swayosd-client --brightness lower
```