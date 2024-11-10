# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname="lwjgl"
pkgver="3.3.4"
pkgrel="1"
arch=("any")
pkgdesc="Java library that enables access to OpenGL, OpenAL, Vulkan, and more."
url="https://github.com/LWJGL/lwjgl3"
source=(
  "$url/archive/refs/tags/$pkgver.tar.gz"
  0001-disable-awt-in-build.patch
  0002-disable-remotery-in-build.patch
  gcc.patch
  libgl.patch
  fix-implicit-conversion-in-pars.patch
)
sha256sums=("SKIP" "SKIP" 'SKIP' 'SKIP' "SKIP" 'SKIP')
options=("!strip")
license=("BSD")
depends=("java-runtime" "dbus" "gtk3")
makedepends=("java-environment" "ant" "linux-headers")

prepare() {
  _patch_ lwjgl3-$pkgver
}

build() {
  cd lwjgl3-$pkgver
  export JAVA_HOME=/usr/lib/jvm/java-23-openjdk
  ant compile-templates
  ant compile

  ant compile-native
}

package() {
  install -d "$pkgdir"/usr/share/java/lwjgl
  install -m 644 "$srcdir"/lwjgl-$pkgver/lwjgl-$pkgver/lib/lwjgl-all-$pkgver.jar "$pkgdir"/usr/share/java/lwjgl/lwjgl-all-$pkgver.jar

  ln -s lwjgl-all-$pkgver.jar "$pkgdir"/usr/share/java/lwjgl/lwjgl-all.jar

  cp --no-preserve=ownership "$srcdir/lwjgl-$pkgver/lib"/*.jar "$pkgdir"/usr/share/java/lwjgl/
}

