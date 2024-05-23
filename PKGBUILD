# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>

pkgname=publicsuffix-list
_gitcommit=0ed17ee161ed2ae551c78f3b399ac8f2724d2154
pkgver=20240513.1499.0ed17ee
pkgrel=1
pkgdesc='Cross-vendor public domain suffix database'
url='https://github.com/publicsuffix/list'
arch=('any')
license=('custom:MPL2')
makedepends=('git')
source=(${pkgname}::"git+https://github.com/publicsuffix/list#commit=${_gitcommit}")
sha512sums=('SKIP')

pkgver() {
  cd ${pkgname}
  printf "%s.%s.%s" "$(TZ=UTC git show -s --pretty=%cd --date=format-local:%Y%m%d HEAD)" \
    "$(git rev-list --count HEAD)" \
    "$(git rev-parse --short HEAD)"
}

package() {
  cd ${pkgname}
  install -Dm 644 public_suffix_list.dat tests/test_psl.txt -t "${pkgdir}/usr/share/publicsuffix"
  ln -s public_suffix_list.dat "${pkgdir}/usr/share/publicsuffix/effective_tld_names.dat"
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
