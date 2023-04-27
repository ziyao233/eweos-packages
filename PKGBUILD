# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=lcms2
pkgver=2.15
pkgrel=1
pkgdesc='Small-footprint color management engine, version 2'
arch=('x86_64' 'aarch64')
url='http://www.littlecms.com/'
license=('MIT')
depends=('libtiff')
source=("https://github.com/mm2/Little-CMS/releases/download/lcms${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha256sums=('b20cbcbd0f503433be2a4e81462106fa61050a35074dc24a4e356792d971ab39')

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
