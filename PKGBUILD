# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=pkcs11-helper
pkgver=1.31.0
pkgrel=3
pkgdesc='A library that simplifies the interaction with PKCS11 providers for end-user applications using a simple API and optional OpenSSL engine'
arch=(x86_64 aarch64 riscv64 loongarch64)
url='https://github.com/OpenSC/pkcs11-helper'
license=('GPL' 'BSD')
depends=('nss' 'openssl')
provides=('libpkcs11-helper.so')
# 0001: Backport upstream commit 59cc22b8d656 to parse certificate expiration
#       with ASN1_TIME_to_tm() now that ASN1_TIME is opaque in OpenSSL 4.
source=("https://github.com/OpenSC/${pkgname}/releases/download/${pkgname}-${pkgver}/${pkgname}-${pkgver}.tar.bz2"
        0001-crypto-openssl-use-ASN1_TIME_to_tm.patch)
sha256sums=('46f0067bccd7be2c28f88b8bca775172b9e52fb6fc1280b44ca8bb831433fef9'
            'f9c6e84e23ab9884033d2a1797a7e5c42ad071c2f7707852a793d1814ca30ca8')

prepare() {
  _patch_ "$pkgname-$pkgver"
}

build() {
  cd pkcs11-helper-$pkgver

  libtoolize
  aclocal
  autoheader
  automake --add-missing
  autoreconf -v
  ./configure --prefix=/usr
  make
}

package() {
  cd pkcs11-helper-$pkgver

  make DESTDIR="$pkgdir" install
  mkdir -p "$pkgdir"/usr/share/licenses/$pkgname/
  install -D -m0644 COPYING* "$pkgdir"/usr/share/licenses/$pkgname/
}

