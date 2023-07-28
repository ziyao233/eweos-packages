# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=rust
pkgver=1.71.0
pkgrel=1
pkgdesc="Systems programming language focused on safety, speed and concurrency"
arch=(x86_64 aarch64 riscv64)
url='https://www.rust-lang.org/'
license=(MIT Apache)
source=(
  https://static.rust-lang.org/dist/rustc-$pkgver-src.tar.gz
  config.toml.x86_64
  config.toml.aarch64
  do-not-use-lfs64.patch
)
sha256sums=('a667e4abdc5588ebfea35c381e319d840ffbf8d2dbfb79771730573642034c96'
            '6ae6ca31ab75bd9474a0f9edf2431630603cb4db475edc6e15a41793861d9615'
            'b03d82b27697e7c6851ead47e8eca74458ad3a34f3ba8663d6216fdecf4025c0'
            'b19e0ce87427426a30b579ebc0a02ada54d9bd3fd920392d82d97149da8ef65a')

depends=(musl llvm-libs musl-static curl libssh2)
makedepends=(rust llvm libffi perl python cmake ninja)

prepare()
{
  cd ${pkgname}c-$pkgver-src

  # https://github.com/rust-lang/rust/pull/106246
  patch -p1 < ../do-not-use-lfs64.patch
}

build()
{
  cp config.toml.${CARCH} ${pkgname}c-${pkgver}-src/config.toml

  cd ${pkgname}c-${pkgver}-src

  sed -i "s@%RUSTVER%@$pkgver@g" config.toml

  export RUST_BACKTRACE=1

  DESTDIR="$srcdir/install" python ./x.py install -j "$(nproc)"
}

package()
{
  provides=(cargo rustfmt)
  cp -r $srcdir/install/* "$pkgdir"

  rm $pkgdir/usr/lib/rustlib/{components,install.log,rust-installer-version,uninstall.sh}
  rm $pkgdir/usr/lib/rustlib/manifest-*

  install -d $pkgdir/usr/share/bash-completion
  install -d $pkgdir/usr/share/licenses/rust
  mv -t $pkgdir/usr/share/licenses/rust $pkgdir/usr/share/doc/rust/LICENSE*
}
