# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgbase=libxml2
pkgname=(
  libxml2
  libxml2-docs
)
_pkgver_major=2.13
_pkgver_minor=2
pkgver=${_pkgver_major}.${_pkgver_minor}
pkgrel=1
pkgdesc="XML parsing library, version 2"
arch=(x86_64 aarch64 riscv64)
license=('MIT')
depends=('zlib' 'ncurses' 'xz' 'icu')
makedepends=('python')
url="http://www.xmlsoft.org/"
source=(https://download.gnome.org/sources/${pkgbase}/${_pkgver_major}/${pkgbase}-${pkgver}.tar.xz)
md5sums=('b678709cd8f6bed9980007b8228804a3')

build()
{
  cd ${pkgbase}-${pkgver}
  autoreconf
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --with-threads \
    --with-history \
    --with-icu \
    --with-python=/usr/bin/python
  make
}

check() {
  cd ${pkgbase}-${pkgver}
  make check
}

package_libxml2()
{
  cd ${pkgbase}-${pkgver}
  make DESTDIR="${pkgdir}" install

  mkdir -p ../doc/usr/share
  mv "$pkgdir"/usr/share/{doc,gtk-doc} -t ../doc/usr/share
}

package_libxml2-docs() {
  pkgdesc+=" (documentation)"
  depends=()

  mv doc/* "$pkgdir"
}
