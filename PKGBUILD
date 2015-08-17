# Maintainer: perlawk
pkgname=shark-svn
pkgver=3
pkgrel=3
pkgdesc="SHARK is a fast, modular, feature-rich open-source C++ machine learning library. It provides methods for linear and nonlinear optimization, kernel-based learning algorithms, neural networks, and various other machine learning techniques."
arch=('x86_64' 'i686')
url="http://image.diku.dk/shark/sphinx_pages/build/html/index.html"
license=('GPL3')
groups=()
depends=('boost')
makedepends=('subversion')
install=
source=(CMakeLists.txt)
noextract=()
md5sums=('fc3bbccf18a6796d6575d9f3e2d88ae5')
options=('staticlibs')

_svntrunk=https://svn.code.sf.net/p/shark-project/code/trunk/Shark
_svnmod=shark

prepare() {
	msg "Connecting to SVN server...."

	if [[ -d "$_svnmod/.svn" ]]; then
		(cd "$_svnmod" && svn up -r "$pkgver")
	else
		svn co "$_svntrunk"
	fi

	msg "SVN checkout done or server timeout"
}

build() {
	msg "Starting build..."
	
  mkdir -p "$srcdir"/build
  cd "$srcdir"/build
	cp "$srcdir"/CMakeLists.txt "$srcdir"/Shark
	cd ../Shark
  make -j8
}

package() {
  cd "$srcdir"/Shark
	mkdir -p "$pkgdir"/usr
  make DESTDIR="$pkgdir/" install
	rm -rf "$pkgdir"/usr/share/shark
}
