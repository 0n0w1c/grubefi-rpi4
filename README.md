# grubefi-rpi4
Grubefi your Pi

A PKGBUILD for Manjaro ARM RPi4 images. \
It will convert a RPi4 from booting via firmware to UEFI and grub. \
It also will revert back to firmware upon removal. \
You can install and remove at will, with or without rebooting.
 
Minimal change to how a Manjaro ARM RPi4 installation is maintained. \
The exception is the addition of the `update-grubefi` command, \
which should be run after making boot configuration changes.

Installation

1) A fresh installation is recommended, updated to arm-testing
 
2) sudo pacman -S linux-rpi4-mainline linux-rpi4-mainline-headers
 
3) Download the PKGBUILD or git clone https://github.com/0n0w1c/grubefi-rpi4.git
 
4) makepkg
 
5) sudo pacman -U grubefi-rpi4-x.y-z-aarch64.pkg.tar.zst
 
6) Configure the UEFI on reboot, after each install/upgrade:
   - disable the 3GB limit
   - most importantly, set ACPI + Devicetree
   - boot order (if needed)
 
It is a bit slow to boot with a SD, be patient.
