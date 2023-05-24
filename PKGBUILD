# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: xRemaLx <anton.komolov@gmail.com>

pkgname=perl-module-build-tiny
_pkgname=Module-Build-Tiny
pkgver=0.039
pkgrel=9
pkgdesc="A tiny replacement for Module::Build"
arch=('any')
license=('PerlArtistic' 'GPL')
options=('!emptydirs')
depends=('perl' 'perl-extutils-config' 'perl-extutils-helpers' 'perl-extutils-installpaths')
url="https://search.cpan.org/dist/Module-Build-Tiny"
source=("https://search.cpan.org/CPAN/authors/id/L/LE/LEONT/${_pkgname}-${pkgver}.tar.gz")
sha512sums=('26ca6fe4c1792b26bb2b4711035847f4215ea7c37234fbe24fc07432682fd9d3b6016dbdb2ecb455a7b13f6bea13994826c7f84f21075f0a6e575fa74672903a')

build()
{
  (
    export PERL_MM_USE_DEFAULT=1 PERL5LIB="" \
      PERL_AUTOINSTALL=--skipdeps \
      PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
      PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
      MODULEBUILDRC=/dev/null \
      CFLAGS="$CFLAGS -D_LARGEFILE64_SOURCE"

    cd "${srcdir}/${_pkgname}-${pkgver}"
    /usr/bin/perl Build.PL
    ./Build
  )
}

check()
{
  cd "${srcdir}/${_pkgname}-${pkgver}"
  (
    export PERL_MM_USE_DEFAULT=1 PERL5LIB="" CFLAGS="$CFLAGS -D_LARGEFILE64_SOURCE"
    ./Build test
  )
}

package()
{
  cd "${srcdir}/${_pkgname}-${pkgver}"
  (
    export PERL_AUTOINSTALL=--skipdeps \
      PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
      PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
      CFLAGS="$CFLAGS -D_LARGEFILE64_SOURCE"
    ./Build install
  )
  find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
}
