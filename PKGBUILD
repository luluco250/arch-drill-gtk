# Maintainer: Lucas Melo <luluco250@gmail.com>

pkgname='drill-git'
pkgver=20190513231129_dd220cf
pkgrel=1
epoch=
pkgdesc='GTK+ tool for searching files without indexing, but clever crawling.'
arch=('i686' 'x86_64')
url='https://www.drill.santamorena.me/'
license=('GPL2')

depends=('gtk3')
makedepends=('dub')
provides=('drill')
conflicts=('drill')

source=(
	'git://github.com/yatima1460/Drill.git'
	'git://github.com/yatima1460/GtkD.git'
	'https://github.com/yatima1460/datefmt.git'
)
md5sums=(
	'SKIP'
	'SKIP'
	'SKIP'
)

prepare() {
	cd "${srcdir}/Drill"
	git submodule init
	git config submodule.GtkD.url $srcdir/GtkD
	git config submodule.datefmt.url $srcdir/datefmt
	git submodule update
}

pkgver() {
	cd "${srcdir}/Drill"
	git describe --tags | sed 's/-/_/g'
}

build() {
	cd "${srcdir}/Drill"
	dub build -c GTK -b release
}

package() {
	cd "${srcdir}/Drill"
	chmod +x Drill-GTK
	mkdir -p $pkgdir/opt/Drill
	cp Drill-GTK $pkgdir/opt/Drill
	cp -R assets/ $pkgdir/opt/Drill/assets
	mkdir -p $pkgdir/usr/bin
	cp "../../drill-gtk.sh" $pkgdir/usr/bin/drill-gtk
}