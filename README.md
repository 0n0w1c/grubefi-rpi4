# grubefi-rpi4
![grub2](https://user-images.githubusercontent.com/47831850/134357018-3530c95c-e774-45e7-af97-f830882b6a62.jpg)
#### Grubefi your Pi ####

An experimental PKGBUILD for Manjaro ARM RPi4 installations. \
It will convert a RPi4 from booting via firmware to UEFI and grub. \
And when removed, it will revert to firmware. \
You can install and remove at will, with or without rebooting.
 
Minimal change to how a Manjaro ARM RPi4 installation is maintained. \
The exception is the addition of the `update-grubefi` command, \
which can be used to manually update boot configuration changes to UEFI. \
In most situations, the boot configuration will update automatically. \
The boot configuration being config.txt, cmdline.txt, and overlays.

- - - -
#### Installation ####

1) A fresh installation is recommended, updated to arm-testing
 
2) sudo pacman -S linux-rpi4-mainline linux-rpi4-mainline-headers
 
3) `git clone https://github.com/0n0w1c/grubefi-rpi4.git`
 
4) makepkg -sic
 
5) Configure the UEFI on reboot, after each install/upgrade

Important: The UEFI Firmware (RPI_EFI.fd) saves the settings in the file itself. \
Each time the firmware is installed/upgraded, all settings will be reset to their default. \
You will need to (re)configure the following:
  - set boot order (if needed)

- - - -
#### Guide to the UEFI Firmware ####
Press <kbd>Esc</kbd> when you see the Raspberry

The following Settings changes are pre-applied: \
`Device Manager` → `Raspberry Pi Configuration` → `Advanced Configuration`

Limit RAM to 3GB - Press <kbd>Enter</kbd> Disabled <kbd>Enter</kbd> \
System Table Selection - Press <kbd>Enter</kbd> ACPI + Devicetree <kbd>Enter</kbd>
 - Press <kbd>F10</kbd> to save
 - Press <kbd>Y</kbd> to confirm
 - Press <kbd>Esc</kbd> multiple times to return to the main menu

`Reset`
 - Press <kbd>Enter</kbd>


Boot Order is set to SD → USB → Network.
   
Press <kbd>Esc</kbd> when you see the Raspberry

 `Boot Maintenance Manager` → `Boot Options` → `Change Boot Order`
 - Press <kbd>Enter</kbd>
 - Press <kbd>↑</kbd><kbd>↓</kbd> to highlight your boot device, likely SD/MMC
 - Press <kbd>+</kbd> multiple times to move it to the top of the list
 - Press <kbd>Enter</kbd>
 - Press <kbd>F10</kbd> to save
 - Press <kbd>Y</kbd> to confirm
 - Press <kbd>Esc</kbd> multiple times to return to the main menu

`Reset`
   - Press <kbd>Enter</kbd>

For more information refer to the [README.md](https://github.com/pftf/RPi4/blob/master/Readme.md "RPi4 UEFI").

- - - -
#### Release Notes ####
Raspberry Pi 4 UEFI Firmware version 1.31

Added `efivarfs` to `MODULES=()` in /etc/mkinitcpio.conf

The Boot Order is set to SD → USB → Network

Limit RAM to 3GB set to `Disabled`

System Table Selection set to `ACPI + Devicetree`

The headphone jack is enabled, to better mimic booting via the RPi4 firmware.

grub-mkconfig will run each time update-grubefi is executed.

It is a bit slow to boot with an SD card, be patient.

The fat32 partition, mounted as /boot/efi is considered the UEFI sandbox. \
Do not store your files in this location. All files in /boot/efi/ will be deleted \
upon removal of the this package with `pacman -R grubefi-rpi4`.

Warning: DO NOT have a shell (terminal) or files, open in /boot or /boot/efi during \
the installation or removal processes.

#### Warning: This is EXPERIMENTAL software, total data loss is a real possibility. ####
