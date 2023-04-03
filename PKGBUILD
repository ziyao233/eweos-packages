# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=mold
pkgver=1.9.0
pkgrel=3
pkgdesc='A Modern Linker'
arch=('x86_64' 'aarch64')
url='https://github.com/rui314/mold'
license=('AGPL3')
depends=('musl' 'mimalloc' 'openssl' 'zlib' 'cmake')
makedepends=('python' 'lld')
source=("$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('faf381ba268e714bec7f872de0dd6ea9187ae20b4e12c434a67ac92854701280')

build()
{
  cmake \
    -S "$pkgname-$pkgver" \
    -B build \
    -D CMAKE_BUILD_TYPE='None' \
    -D CMAKE_INSTALL_PREFIX='/usr' \
    -D CMAKE_INSTALL_LIBEXECDIR='lib' \
    -D CMAKE_INSTALL_LIBDIR='lib' \
    -D MOLD_USE_SYSTEM_MIMALLOC=ON \
    -D MOLD_USE_MIMALLOC=0 \
    -D MOLD_USE_MOLD=ON
  cmake --build build
}

package()
{
  DESTDIR="$pkgdir" cmake --install build
  ln -s mold "${pkgdir}/usr/bin/ld"
}
