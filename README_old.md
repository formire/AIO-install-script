# AIO-install-script
Setup script for a fresh Linux install that sets up a system like I may normally use it

## To-Do
- Implement Windows 10 VM via looking-glass and QEMU/KVM (win10)
- Implement macOS VM via Reims-vGPU (macos)
- Implement option(s) to run Android apps (droid)
- Implement Desktop Environment setup
- Implement Disk partitioning (see other sections (*))

### win10
- Add automated GPU detection for proper looking-glass installation (tested on Q538EI and 5,1MacPro (RX 480 + GTX1050Ti), both on Arch Linux)
- Add toggle between disk image/disk partition/separate disk (for dual-booting)
- Create two instances for VM (passthru and no-passthru)

### macos
- Add automated install for Reims-vGPU
- implement disk image/disk partition/separate disk (same as win10)
- Create two instances for VM (passthru and no-passthru)

### droid
- Add menu to choose between waydroid/brunch
- Add brunchVM implementation
- Create two instances for VM (passthru and no-passthru) (needs to be tested first)

### Desktop Environment
- Add common Linux DE's and option to import dotfiles (sway & hyprland)

### Disk partitioning
- Option to split install partition (commonly sda2) into 2/3/4 for dual/multiboot
- Detect ext4 mounted system and halt (done)
- Detect ext4 unmounted system and proceed (only if disk isn't the one the script is running on i.e. Live USB)
