# Maintainer : Yukari Chiba <i@0x7f.cc>

pkgname=connman
pkgver=1.42
pkgrel=1
pkgdesc="Intel's modular network connection manager"
url="https://01.org/connman"
arch=('x86_64' 'aarch64' 'riscv64')
license=('GPL2')
depends=('dbus' 'glib' 'nftables')
optdepends=('wpa_supplicant: for wireless network support')
makedepends=('wpa_supplicant')
source=(
  "${pkgname}-${pkgver}.tar.xz::https://www.kernel.org/pub/linux/network/${pkgname}/${pkgname}-${pkgver}.tar.xz"
  musl-res-ninit.patch
  connman.service
)
sha256sums=('a3e6bae46fc081ef2e9dae3caa4f7649de892c3de622c20283ac0ca81423c2aa'
            '9b006bcf19c461d298d61ee8015263063197c7480c0bf629b9c7ad34bcffbb53'
            '6d3c790d9214cacb8233065fb57cd536e546012659aede772224f128c736a66b')

prepare() {
  cd "${pkgname}-${pkgver}"
  patch -p1 < ../musl-res-ninit.patch
  sed -i '1s/^/#include<stdio.h>\n/' src/dnsproxy.c
}

build() {
  cd "${pkgname}-${pkgver}"

  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
      --bindir=/usr/bin \
      --sbindir=/usr/bin \
      --enable-client \
      --enable-nmcompat \
      --enable-test \
      --with-firewall=nftables \
      --disable-wispr
  make
}

package() {
  make -C "${pkgname}-${pkgver}" DESTDIR="${pkgdir}" install
  install -Dm755 "${srcdir}/${pkgname}-${pkgver}/client/${pkgname}ctl" "${pkgdir}/usr/bin/${pkgname}ctl"
  install -Dm644 "${srcdir}/${pkgname}-${pkgver}/src/main.conf" "${pkgdir}/etc/connman/main.conf"

  _dinit_install_services_ connman.service
}
