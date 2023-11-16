# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgbase=fakeroot
pkgname=(fakeroot fakeroot-tcp)
pkgver=1.32.2
pkgrel=1
pkgdesc='Tool for simulating superuser privileges'
arch=(x86_64 aarch64 riscv64)
license=('GPL')
url='https://tracker.debian.org/pkg/fakeroot'
groups=('base-devel')
depends=('musl' 'filesystem' 'util-linux')
makedepends=('libcap')
source=("https://deb.debian.org/debian/pool/main/f/$pkgname/${pkgname}_${pkgver}.orig.tar.gz" musl.patch xstatjunk.patch)
sha256sums=('f0f72b504f288eea5b043cd5fe37585bc163f5acaacd386e1976b1055686116d'
            'baab2d372a484bfd13ce001879c909b44eba65df894696c8dd8b734f1ab36f43'
            '8680c89fe37a75b756585a505a077b26af8a089d05466cbf86522adc81d84e1b')

build()
{
  cd $srcdir/$pkgbase-$pkgver
  patch -p1 < ${srcdir}/musl.patch
  patch -p1 < ${srcdir}/xstatjunk.patch
  autoreconf -fiv
  cp -r $srcdir/$pkgbase-$pkgver $srcdir/$pkgbase-$pkgver-tcp

  cd $srcdir/$pkgbase-$pkgver
  ./configure --prefix=/usr \
    --libdir=/usr/lib/libfakeroot \
    --disable-static \
    --with-ipc=sysv
  make

  cd $srcdir/$pkgbase-$pkgver-tcp
  ./configure --prefix=/usr \
    --libdir=/usr/lib/libfakeroot \
    --disable-static \
    --with-ipc=tcp
  make
}

package_fakeroot()
{
  provides=($pkgbase)
  conflicts=($pkgbase)
  cd $srcdir/$pkgbase-$pkgver
  make DESTDIR="$pkgdir" install

  install -dm0755 "$pkgdir/etc/ld.so.conf.d/"
  echo '/usr/lib/libfakeroot' > "$pkgdir/etc/ld.so.conf.d/fakeroot.conf"
}

package_fakeroot-tcp()
{
  pkgdesc="$pkgdesc (TCP IPC)"
  provides=($pkgbase)
  conflicts=($pkgbase)
  cd $srcdir/$pkgbase-$pkgver-tcp
  make DESTDIR="$pkgdir" install

  install -dm0755 "$pkgdir/etc/ld.so.conf.d/"
  echo '/usr/lib/libfakeroot' > "$pkgdir/etc/ld.so.conf.d/fakeroot.conf"
}
