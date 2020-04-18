# Maintainer: Chih-Hsuan Yen <yan12125@gmail.com>
# Contributor: Yushin Huang <hyslion AT gmail.com>

_pkgname=libchewing
pkgname=libchewing-git-cmkdh
pkgver=0.5.1.r106.g2ebcf13
pkgrel=1
epoch=1
pkgdesc='Intelligent Chinese phonetic input method'
url='http://chewing.im/'
arch=('i686' 'x86_64')
license=('LGPL2.1')
conflicts=("$_pkgname")
provides=("$_pkgname=$pkgver")
depends=('sqlite')
makedepends=('cmake' 'git')
source=("git+https://github.com/chewing/libchewing/" "colemakdh.patch")
md5sums=('SKIP' 'SKIP')

pkgver() {
  cd "$_pkgname"
  ( set -o pipefail
    git describe --long --tag 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//'
  )
}

prepare() {
  cd "$_pkgname"
  patch -p1 < ../colemakdh.patch
  rm -rf build
  mkdir build
}

build() {
  cd $_pkgname/build
  cmake \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=/usr/lib \
    ..
  make
}

check() {
  cd $_pkgname/build
  # parallel testing is broken (https://github.com/chewing/libchewing/issues/293)
  make -j1 check
}

package() {
  cd $_pkgname/build
  make DESTDIR="$pkgdir" install
}
