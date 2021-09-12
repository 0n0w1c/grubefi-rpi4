pkgname=grubefi-rpi4
pkgver=1.3
pkgrel=3
uefiver=1.31
pkgdesc="Grub-efi your Pi (4B/400/CM4)"
arch=('aarch64')
url="https://github.com/0n0w1c/grubefi-rpi4"
license=('MIT')
depends=('grub')
provides=('grubefi-rpi4')
conflicts=()
options=('!strip')
install=grubefi-rpi4.install
source=("https://github.com/pftf/RPi4/releases/download/v$uefiver/RPi4_UEFI_Firmware_v$uefiver.zip"
        "https://github.com/0n0w1c/grubefi-rpi4/blob/master/95-update-grubefi.hook"
        "https://github.com/0n0w1c/grubefi-rpi4/blob/master/update-grubefi"
        "https://github.com/0n0w1c/grubefi-rpi4/blob/master/grubefi-rpi4.install")

md5sums=('0a391d5e0ddbde8f017317e0be0c9b2f'
         'b5c131863bb4bb4b7878988e5ddc12e4'
         'fab4d7b5e2367a7fc748b1117a51973f'
         '8c554c0e5a2e3233253905db1d0d47ec')

package() {
   mkdir -p $pkgdir/boot/efi
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
   cp RPI_EFI.fd $pkgdir/boot/efi/
   cp config.txt $pkgdir/boot/efi/config.txt.uefi

   cp 95-update-grubefi.hook $pkgdir/usr/share/libalpm/hooks/

   cp update-grubefi $pkgdir/usr/bin/
   chmod 755 $pkgdir/usr/bin/update-grubefi
}
