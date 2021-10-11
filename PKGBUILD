pkgname=grubefi-rpi4
pkgver=1.10
pkgrel=4
uefiver=1.31
pkgdesc="grubefi your pi (4B/400/CM4)"
arch=('aarch64')
url="https://github.com/0n0w1c/grubefi-rpi4"
license=('MIT')
depends=('bsdiff' 'grub' 'grub-theme-vimix' 'manjaro-arm-wallpapers')
provides=('grubefi-rpi4')
conflicts=()
options=('!strip')
install=grubefi-rpi4.install
source=("https://github.com/pftf/RPi4/releases/download/v$uefiver/RPi4_UEFI_Firmware_v$uefiver.zip"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/RPI_EFI.fd.patch"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/95-update-grubefi.hook"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/update-grubefi"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/grubefi-rpi4.install"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/watch-cmdline.path"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/watch-cmdline.service"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/watch-config.path"
        "https://raw.githubusercontent.com/0n0w1c/$pkgname/master/watch-config.service")

md5sums=('0a391d5e0ddbde8f017317e0be0c9b2f'
         '6cc108582dcf6eb9d8d0586b858a2b8b'
         'dd46de30c86b872cee5e729a71a4de72'
         '1e45ba0f5092c3714c88297273183276'
         'e8154e17fd44ee949cd1d2a506b161ab'
         '780f27cc63514018f4fc373dbba91b3f'
         '9b4afbca83c63b826416187809cb3d1e'
         '027254ce97c7b50485a5854b989ec876'
         '9b4afbca83c63b826416187809cb3d1e')

package() {
   install -D bcm2711-rpi-400.dtb $pkgdir/boot/efi/bcm2711-rpi-400.dtb
   install -D bcm2711-rpi-4-b.dtb $pkgdir/boot/efi/bcm2711-rpi-4-b.dtb
   install -D bcm2711-rpi-cm4.dtb $pkgdir/boot/efi/bcm2711-rpi-cm4.dtb

   find overlays -type f -exec install -D "{}" "$pkgdir/boot/efi/{}" \;
   find firmware -type f -exec install -D "{}" "$pkgdir/boot/efi/{}" \;

   install -D start4.elf $pkgdir/boot/efi/start4.elf
   install -D fixup4.dat $pkgdir/boot/efi/fixup4.dat
   install -D Readme.md $pkgdir/boot/efi/Readme.md

   #install -D RPI_EFI.fd $pkgdir/boot/efi/RPI_EFI.fd
   bspatch RPI_EFI.fd $pkgdir/boot/efi/RPI_EFI.fd RPI_EFI.fd.patch

   sed -i -e 's/^uart_2ndstage=1/#uart_2ndstage=1/' config.txt
   sed -i -e 's/^dtoverlay=miniuart-bt/#dtoverlay=miniuart-bt/' config.txt
   sync
   install -D config.txt $pkgdir/boot/efi/config.txt.uefi

   install -Dm 644 watch-cmdline.path $pkgdir/etc/systemd/system/watch-cmdline.path
   install -Dm 644 watch-cmdline.service $pkgdir/etc/systemd/system/watch-cmdline.service
   install -Dm 644 watch-config.path $pkgdir/etc/systemd/system/watch-config.path
   install -Dm 644 watch-config.service $pkgdir/etc/systemd/system/watch-config.service

   install -Dm 644 95-update-grubefi.hook $pkgdir/usr/share/libalpm/hooks/95-update-grubefi.hook

   install -Dm 755 update-grubefi $pkgdir/usr/bin/update-grubefi
}
