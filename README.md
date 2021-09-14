# grubefi-rpi4
Grubefi your Pi

An experimental PKGBUILD for Manjaro ARM RPi4 installations. \
It will convert a RPi4 from booting via firmware to UEFI and grub. \
And when removed, it will revert to firmware. \
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

Guide to the UEFI Firmware:
Press [Esc] when you see the Raspberry

Device Manager -> Raspberry Pi Configuration -> Advanced Configuration
Limit RAM to 3GB Press [Enter] <Disabled> [Enter]
System Table Selection Press [Enter] <ACPI + Devicetree> [Enter]
   - Press [F10] to Save
   - Press [Y] to confirm
   - Press [Esc] multiple times to return to the main menu
Reset
   - Press [Enter]

SSD seem to be placed first in the boot order (if so, skip this).
If using a SD Card, you will also want to set the Boot Order.
By default, the SD/MMC is set to last, after long network timeouts.
   
Press [Esc] when you see the raspberry
Boot Maintenance Manager -> Boot Options -> Change Boot Order
   - Press [Up/Down] to highlight your boot device, likely SD/MMC
   - Press [+] multiple times to move it to the top of the list
   - Press [Enter]
   - Press [F10] to Save
   - Press [Y] to confirm
   - Press [Esc] multiple times to return to the main menu
Reset
   - Press [Enter]

It is a bit slow to boot with an SD card, be patient.

Warning: Do NOT have a shell or files open in /boot or /boot/efi during \
the installation or removal process.

Warning: This is EXPERIMENTAL software, total data loss is a real possibility.

Note: Due to an issue with a hanging process during shutdown/reboot when \
bluetooth is enabled, bluetooth has been disabled.
