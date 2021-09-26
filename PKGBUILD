pkgname=grubefi-rpi4
pkgver=1.7
pkgrel=2
uefiver=1.31
pkgdesc="grubefi your pi (4B/400/CM4)"
arch=('aarch64')
url="https://github.com/0n0w1c/grubefi-rpi4"
license=('MIT')
depends=('bsdiff' 'grub' 'grub-theme-vimix' 'lsof' 'manjaro-arm-wallpapers')
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
         '714fffcafca72edf2ae94bf768fa1321'
         'dd46de30c86b872cee5e729a71a4de72'
         '342e29a3179268f3d599eb5f7d204a39'
         '48ae0e6fcf21128c60825366fdd9d05b'
         '780f27cc63514018f4fc373dbba91b3f'
         'e3086a7d5c1dea1aeaed1674ccbbe176'
         '027254ce97c7b50485a5854b989ec876'
         'e3086a7d5c1dea1aeaed1674ccbbe176')

package() {
   mkdir -p $pkgdir/boot/efi
   mkdir -p $pkgdir/etc/systemd/system/
   mkdir -p $pkgdir/usr/share/libalpm/hooks
   mkdir -p $pkgdir/usr/bin

   cp bcm2711-rpi-400.dtb $pkgdir/boot/efi/
   cp bcm2711-rpi-4-b.dtb $pkgdir/boot/efi/
   cp bcm2711-rpi-cm4.dtb $pkgdir/boot/efi/
   cp -r overlays $pkgdir/boot/efi/
   cp -r firmware $pkgdir/boot/efi/
   cp start4.elf $pkgdir/boot/efi/
   cp fixup4.dat $pkgdir/boot/efi/
   cp Readme.md $pkgdir/boot/efi/
   #cp RPI_EFI.fd $pkgdir/boot/efi/
   bspatch RPI_EFI.fd $pkgdir/boot/efi/RPI_EFI.fd RPI_EFI.fd.patch
   cp config.txt $pkgdir/boot/efi/config.txt.uefi

   cp watch-cmdline.path $pkgdir/etc/systemd/system/
   cp watch-cmdline.service $pkgdir/etc/systemd/system/
   cp watch-config.path $pkgdir/etc/systemd/system/
   cp watch-config.service $pkgdir/etc/systemd/system/

   cp 95-update-grubefi.hook $pkgdir/usr/share/libalpm/hooks/

   cp update-grubefi $pkgdir/usr/bin/
   chmod 755 $pkgdir/usr/bin/update-grubefi
}
