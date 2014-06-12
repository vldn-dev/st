# $Id: PKGBUILD 60970 2011-12-19 21:33:58Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Dag Odenhall <dag.odenhall@gmail.com>
# Contributor: Grigorios Bouzakis <grbzks@gmail.com>

pkgname=st
pkgver=0.5
pkgrel=1
pkgdesc="A symple virtual terminal emulator for X. X"
url="http://st.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libxext' 'libxft')
makedepends=('ncurses')
source=(http://dl.suckless.org/st/st-$pkgver.tar.gz
config.h)
_patches=()
md5sums=('4f8ae2737120a8cba34b23c6020fe51e'
         '649a057449c5f34c42e2eac649c71a20')

source=(${source[@]} ${_patches[@]})
build() {
	cd $srcdir/$pkgname-$pkgver
	for p in "${_patches[@]}"; do
		echo "=> $p"
		patch < ../$p || return 1
	done
	cp $srcdir/config.h config.h
	sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
	sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
	sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
	sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
	sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd $srcdir/$pkgname-$pkgver
	make PREFIX=/usr DESTDIR=$pkgdir install
	install -m644 -D LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
	install -m644 -D README $pkgdir/usr/share/doc/$pkgname/README
}
