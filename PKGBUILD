# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=utmps
pkgver=0.1.2.0
pkgrel=1
pkgdesc='An implementation of the utmpx.h family of functions performing user accounting'
arch=(x86_64)
url='http://skarnet.org/software/utmps/'
license=(ISC)
groups=()
depends=(dinit)
makedepends=(skalibs)
options=()

source=(
    "http://skarnet.org/software/utmps/utmps-${pkgver}.tar.gz"
    utmpd.service
    wtmpd.service
    utmps.install
)

sha256sums=(
    'SKIP'
    'SKIP'
    'SKIP'
    'SKIP'
)

install=utmps.install

build() {
    cd ${pkgname}-${pkgver}
    ./configure \
        --prefix=/usr \
        --bindir=/usr/bin \
        --libdir=/usr/lib \
        --with-sysdeps=/usr/lib/skalibs/sysdeps \
        --enable-libc-includes
    make
}

package() {
    cd ${pkgname}-${pkgver}
    make DESTDIR=${pkgdir} install
    install -d "${pkgdir}/etc/dinit.d"
    install "${srcdir}/utmpd.service" "${pkgdir}/etc/dinit.d/utmpd"
    install "${srcdir}/wtmpd.service" "${pkgdir}/etc/dinit.d/wtmpd"
}

