# Maintainer: Christian Hesse <mail@eworm.de>
# Contributor: mickele <mimocciola at yahoo dot com> (librecad-git PKGBUILD)
# Contributor: Ilmari Repo <ilmari at gmail dot com> (librecad-svn PKGBUILD)
# Contributor: GazJ Gary James <garyjames82 at gmail dot com> (CADuntu PKGBUILD)

pkgname=librecad
pkgver=2.0.7
pkgrel=2
pkgdesc='A 2D CAD drawing tool based on the community edition of QCad'
arch=('i686' 'x86_64')
url='http://www.librecad.org/'
license=('GPL')
depends=('qt5-base' 'qt5-svg' 'qt5-tools' 'libxcb' 'muparser')
makedepends=('boost' 'imagemagick' 'librsvg')
conflicts=('librecad-git')
replaces=('librecad-svn' 'caduntu' 'caduntu-svn')
install=librecad.install
source=("${pkgname}-${pkgver}.tar.gz::https://codeload.github.com/LibreCAD/LibreCAD/tar.gz/${pkgver}")

build() {
	cd "${srcdir}/LibreCAD-${pkgver}"

	# fix version string
	sed -i "/^SCMREVISION/c SCMREVISION=\"${pkgver}\"" librecad/src/src.pro

	export CPPFLAGS="-std=c++0x"
	qmake-qt5 librecad.pro
	make
}

package() {
	cd "${srcdir}/LibreCAD-${pkgver}"

	install -D -m0755 unix/librecad "${pkgdir}/usr/bin/librecad"
	install -D -m0755 unix/ttf2lff "${pkgdir}/usr/bin/ttf2lff"

	install -D -m0644 desktop/librecad.desktop "${pkgdir}/usr/share/applications/librecad.desktop"
	install -D -m0644 desktop/librecad.1 "${pkgdir}/usr/share/man/man1/librecad.1"

	install -D -m0644 librecad/support/doc/README "${pkgdir}/usr/share/doc/librecad/index.README"
	install -D -m0644 librecad/support/doc/index.html "${pkgdir}/usr/share/doc/librecad/index.html"
	install -D -m0644 librecad/support/doc/style.css "${pkgdir}/usr/share/doc/librecad/style.css"
	install -D -m0644 librecad/support/doc/img/librecadlogo.png "${pkgdir}/usr/share/doc/librecad/img/librecadlogo.png"

	for SIZE in 16 24 32 48 64 96 128; do
		convert -scale ${SIZE} \
			desktop/graphics_icons_and_splash/Icon\ LibreCAD/Icon_Librecad.svg \
			${srcdir}/librecad.png
		install -D -m0644 ${srcdir}/librecad.png "${pkgdir}/usr/share/icons/hicolor/${SIZE}x${SIZE}/apps/librecad.png"
	done
	install -D -m0644 desktop/graphics_icons_and_splash/Icon\ LibreCAD/Icon_Librecad.svg "${pkgdir}/usr/share/icons/hicolor/scalable/apps/librecad.svg"

	mkdir -p "${pkgdir}/usr/share/librecad/"
	cp -r unix/resources/{library,patterns,fonts,qm} "${pkgdir}/usr/share/librecad/"
}

sha256sums=('c8ae88be5e2d1cac9c979c2922b52d33d4f156bff63ea217c646f6bc07f88c0d')
