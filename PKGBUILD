# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=foot
pkgdesc='A fast, lightweight and minimalistic Wayland terminal emulator'
pkgver=1.16.2
pkgrel=2
url="https://codeberg.org/dnkl/$pkgname"
arch=(x86_64 aarch64 riscv64)
license=(MIT)
makedepends=(
  meson
  ninja
  python
  tllist
  sway
  scdoc
  wayland
  wayland-protocols
)
depends=(
  fontconfig
  fcft
  libxkbcommon
  ncurses
  pixman
  libutf8proc
  wayland
)
source=("$pkgname-$pkgver.tar.gz::$url/archive/$pkgver.tar.gz")
sha256sums=('8060ec28cbf6e2e3d408665330da4bc48fd094d4f1265d7c58dc75c767463c29')

prepare() {
  sed -i 's/werror=true/werror=false/g' $pkgname/meson.build
}

build() {
  ewe-meson $pkgname build \
    --buildtype=release \
    -D terminfo=disabled
  meson compile -C build
}

check() {
  meson test -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}

