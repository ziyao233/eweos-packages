# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=(binutils-gold binutils-objcopy)
pkgver=2.41
pkgrel=1
pkgdesc='GNU binutils'
url='https://www.gnu.org/software/binutils/'
arch=(x86_64 aarch64 riscv64)
license=(GPL2 GPL3 LGPL2 LGPL3)
depends=(musl)
source=("https://ftp.gnu.org/gnu/binutils/binutils-$pkgver.tar.gz")

build () {
	cd binutils-$pkgver
	cd libsframe && ./configure && make
	cd ../bfd && ./configure --with-system-zlib && make
	cd ../libiberty && ./configure && make
	cd ../gold && ./configure && make
	cd ../binutils && ./configure && make objcopy
}

package_binutils-gold() {
	install -Dm755 binutils-$pkgver/gold/ld-new	\
		$pkgdir/usr/bin/binutils-gold
}

package_binutils-objcopy() {
	install -Dm755 binutils-$pkgver/binutils/objcopy	\
		$pkgdir/usr/bin/binutils-objcopy
}

sha256sums=('48d00a8dc73aa7d2394a7dc069b96191d95e8de8f0da6dc91da5cce655c20e45')
