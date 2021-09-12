# grubefi-rpi4
Grubefi your Pi

An experimental PKGBUILD for Manjaro ARM RPi4 images. \
It will convert a RPi4 from booting via firmware to UEFI and grub. \
It will revert to firmware upon removal. \
You can install and remove at will, with or without rebooting.
 
Minimal change to how a Manjaro ARM RPi4 installation is maintained. \
The exception is the addition of the `update-grubefi` command, \
which should be run after making configuration changes to files in /boot.

Installation

1) A fresh installation is recommended, updated to arm-testing
 
2) sudo pacman -S linux-rpi4-mainline linux-rpi4-mainline-headers
 
3) Download the PKGBUILD or git clone https://github.com/0n0w1c/grubefi-rpi4.git
 
4) makepkg -sic
 
5) Configure the UEFI on reboot, after each install/upgrade:
   - disable the 3GB limit
   - set ACPI + Devicetree
   - boot order
 
It is a bit slow to boot with an SD card, be patient.

Warning: Do NOT have a shell or files open in /boot or /boot/efi during \
the installation or removal process.

Warning: This is EXPERIMENTAL software, total data loss is a real possibility.

Note: Due to an issue with a hanging process during shutdown/reboot with bluetooth \
active, bluetooth has been disabled.
