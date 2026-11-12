# AIO Install Script

An automated setup script for fresh Linux installations. The goal is to automate the installation and configuration of the software, virtual machines, desktop environments, and tools I commonly use.

The project is designed to be modular, allowing users to choose which components they want to install and configure.

> [!WARNING]
> This project is currently under development. Some features are still being tested or have not yet been implemented. Do not use the disk partitioning functionality on a system containing important data without first verifying its behavior and backing up your data.

## Project Status

| Component | Status |
|---|---|
| Windows 10 VM (`redstone.sh`) | Hardware testing completed; automation pending |
| macOS VM (`pearl.sh`) | Reims-vGPU tested; automation pending |
| Android (`aluminium.sh`) | Planned |
| Desktop Environment (`varies by DE`) | Planned |
| Disk Partitioning (`prism.sh`)| Currently testing |

## Supported Hardware

The following systems have been used to test the virtualization configurations. This does not mean the installation script currently supports automatic configuration on these systems.

### ASUS ZenBook Q538EI
- Host OS: Arch Linux
- CPU: Intel Core i7-1165G7
- GPU1: Intel Iris Xe Graphics (iGPU)
- GPU2: NVIDIA GTX 1650 Ti Mobile (dGPU)
- Tested configurations:
  - Dual-GPU Windows 10 VM using QEMU/KVM and Looking Glass.
  - NVIDIA GPU passthrough to the Windows VM.
  - Reims-vGPU without physical GPU passthrough (iGPU).

### Mac Pro 5,1
- Host OS: Arch Linux
- CPU: Dual Intel Xeon processors (E5520).
- GPUs:
  - AMD RX 480 (Windows VM).
  - NVIDIA GTX 1050 Ti (Host).
- Tested configurations:
  - Dual-GPU Windows 10 VM using QEMU/KVM and Looking Glass.
  - Windows 10 installed on a separate physical disk and passed through to the VM.
  - Reims-vGPU without physical GPU passthrough (GTX 1050Ti).
> [!NOTE]
> I am currently testing this script to also work for ARM64 architecture
> Test devices are Raspberry Pi 4 and M1 MacBook Pro

### Hardware Compatibility

Hardware detection and automatic configuration are planned features. The systems above are testing environments, not a list of supported hardware.

---

## Installation

**Requirements**
- A fresh Linux installation.
- Internet connection.
- Root or sudo.
- Compatible hardware for the features you intend to use.

**Current installation status:** The automated installer is under development. The following is the intended installation workflow and is not yet a guaranteed working procedure.

1. Clone repo:

   ```bash
   git clone https://github.com/formire/AIO-install-script.git
   ```

2. Enter the project directory:

   ```bash
   cd AIO-install-script
   ```

3. Mark as executable:

   ```bash
   chmod +x setup.sh
   ```

4. Run the installer:

   ```bash
   sudo ./setup.sh
   ```

---

## Usage

The intended goal is to provide an interactive menu that allows users to select which components they want to install.

Planned menu structure:

```text
main_menu() {
    while true; do
        printf '\n%s\n' "Formire's AIO Installer"
        printf '  %s Desktop environment setup\n' "$(color_blue '1)')"
        printf '  %s Disk setup\n' "$(color_blue '2)')"
        printf '  %s Windows 10 VM (Looking Glass)\n' "$(color_blue '3)')"
        printf '  %s macOS VM (Reims-vGPU)\n' "$(color_blue '4)')"
        printf '  %s Android apps / OS\n' "$(color_blue '5)')"
        printf '  %s Other features\n' "$(color_blue '6)')"
        printf '  %s Show detected system information\n' "$(color_blue '7)')"
        printf '  %s Refresh cached system information\n' "$(color_blue '8)')"
        printf '  %s Exit\n' "$(color_blue '0)')"
        read -rp "Choose an option: " choice
```
> [!NOTE]
> snippet from `setup.sh` script

Each component will have its own configuration options.

For example, the Windows 10 VM setup will eventually allow users to select:
- GPU passthrough or virtual GPU.
- QCOW2 image, existing partition, or entire physical disk.

The macOS and Android configurations will follow a similar modular approach where applicable.

---

### 1. Windows 10 VM (`redstone.sh`)

**Completed Testing**
- [x] Test dual-GPU Windows 10 VM with Looking Glass on ASUS Q538EI.
- [x] Test dual-GPU Windows 10 VM with Looking Glass on Mac Pro 5,1.
- [x] Test physical disk passthrough using a separate Windows 10 installation on Mac Pro 5,1.
**Testing**
- [ ] ARM64 Architecture
  - [ ] Raspberry Pi 4
  - [ ] M1 MacBook Pro
**To-do**
- [ ] Implement automated GPU detection.
- [ ] Automate Looking Glass installation and configuration.
- [ ] Add storage configuration options:
  - [ ] Virtual disk image (QCOW2).
  - [ ] Existing disk partition.
  - [ ] Entire physical disk.
- [ ] Create two VM configurations:
  - [ ] GPU passthrough.
  - [ ] No GPU passthrough (virtual GPU).
- [ ] Install BIOS files (if GPU needs it)
- [ ] Add "fake battery" for laptop dGPU (Q538EI)

### 2. macOS VM (`pearl.sh`)

**Completed Testing**
- [x] Test Reims-vGPU on ASUS Q538EI.
- [x] Test Reims-vGPU on Mac Pro 5,1.
- [x] Test both configurations without physical GPU passthrough.
**Testing**
- [ ] ARM64 Architecture
  - [ ] Raspberry Pi 4
  - [ ] M1 MacBook Pro
**To-do**
- [ ] Automate Reims-vGPU installation and configuration.
- [ ] Add storage configuration options:
  - [ ] Virtual disk image.
  - [ ] Existing disk partition.
  - [ ] Entire physical disk.
- [ ] Create two VM configurations:
  - [ ] GPU passthrough.
  - [ ] No GPU passthrough (Reims-vGPU).

### 3. Android (`aluminium.sh`)

**Testing**
- [x] Test Waydroid.
- [ ] Test Brunch.

**To-do**
- [ ] Add installation menu to choose between Waydroid and Brunch.
- [ ] Implement Brunch VM support.
- [ ] Investigate GPU acceleration and passthrough compatibility.
  - [ ] Create separate configurations for:
    - [ ] GPU passthrough.
    - [ ] No GPU passthrough.

### 4. Desktop Environment

**To-do**
- [ ] Add installation options for common Linux desktop environments.
- [ ] Add support for importing existing dotfiles.
- [ ] Include configurations for:
  - [ ] i3.
  - [ ] Sway.
  - [ ] Hyprland.
    - [ ] Include option to configure Dusky (Arch only)

### 5. Disk Partitioning (`prism.sh`)

**Currently Testing**
- [ ] Test automatic splitting of an existing installation partition (commonly `sda2`) into 2, 3, or 4 partitions for dual-boot and multiboot configurations.

**Completed**
- [x] Detect mounted ext4 system partitions.
- [x] Halt execution when a mounted ext4 system partition is detected.

**To-do**
- [In progress] Detect unmounted ext4 system partitions.
- [ ] Allow operations on unmounted partitions when safe.
- [ ] Verify that the target disk is not the disk currently running the script (e.g., a Live USB).
- [ ] Add safeguards against accidental modification or formatting of existing installations.

---

| Status | Meaning |
|---|---|
| [x] | Tested / Completed |
| [ ] | Planned / Not yet implemented |
| In Progress | Currently being developed or tested |

- Testing a feature on physical hardware does not necessarily mean its installation and configuration have been automated.
- GPU passthrough and virtual GPU configurations are treated as separate VM implementations.
- Disk operations should include safety checks to prevent accidental modification of existing installations.
- Hardware compatibility will expand as additional systems are tested.
