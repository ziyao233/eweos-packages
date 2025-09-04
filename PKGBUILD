# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=libdyn-crt
pkgver=20.1.8
_llvmver=${pkgver%%.*}
pkgrel=1
pkgdesc='Dynamic library providing compiler-rt symbols'
arch=(x86_64 aarch64 riscv64 loongarch64)
license=('Apache-2.0 WITH LLVM-exception')
depends=(musl)

build() {
	local _clangdir=/usr/lib/clang/$_llvmver/lib/linux

	clang -fPIC -Wl,--no-as-needed -Wl,--whole-archive \
		$_clangdir/libclang_rt.builtins-$CARCH.a	\
		-shared -o libdyn-crt.so -nostdlib
}

package() {
	install -Dm755 libdyn-crt.so -t "$pkgdir"/usr/lib/
}
