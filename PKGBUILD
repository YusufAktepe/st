# Maintainer: Yusuf Aktepe <yusuf@yusufaktepe.com>

_name=st
pkgname=${_name}-git
pkgver=0.8.2.r1091.0d1cde2
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='https://github.com/yusufaktepe/st'
arch=('i686' 'x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
makedepends=('git' 'libxext' 'ncurses')
optdepends=('dmenu: feed urls to dmenu')
source=("${_name}::git+${url}.git")
sha1sums=('SKIP')

provides=("${_name}")
conflicts=("${_name}")

pkgver() {
	cd "${_name}"
	printf "%s.r%s.%s" "$(awk '/^VERSION =/ {print $3}' config.mk)" \
		"$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd "${_name}"
	# skip terminfo which conflicts with ncurses
	sed -i '/tic /d' Makefile
}

build() {
	cd "${_name}"
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${_name}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
