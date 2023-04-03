# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=lcms2
pkgver=2.14
pkgrel=1
pkgdesc='Small-footprint color management engine, version 2'
arch=('x86_64' 'aarch64')
url='http://www.littlecms.com/'
license=('MIT')
depends=('libtiff')
source=("https://github.com/mm2/Little-CMS/releases/download/lcms${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha256sums=('28474ea6f6591c4d4cee972123587001a4e6e353412a41b3e9e82219818d5740')

build() {
  cd "${pkgname}-${pkgver}"
  ./configure --prefix=/usr
  make
}

check() {
  cd "${pkgname}-${pkgver}"
  make check
}

package() {
  cd "${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -D -m0644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
