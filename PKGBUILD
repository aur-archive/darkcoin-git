# Maintainer: Vertoe <vertoe AT darkcoin DOT io>
# Contributor: deusstultus <deusstultus AT gmail DOT com>
# Contributor: Viliam Kubis <viliam DOT kubis AT gmail DOT com>
# Based on PKGBUILD from vertcoin-git maintained by Lothar_m <lothar_m AT riseup DOT net>

pkgname='darkcoin-git'
_gitname='darkcoin'
_gitbranch='master'
pkgver=6333.bdbdbf9
pkgrel=1
arch=('i686' 'x86_64')
url="https://www.darkcoin.io/"
depends=('qt5-base' 'boost' 'boost-libs' 'miniupnpc' 'openssl')
makedepends=('autoconf' 'automake' 'binutils' 'gcc' 'libtool' 'make' 'pkg-config' 'git' 'qrencode' 'automoc4' 'protobuf' 'qt5-tools')
license=('MIT')
pkgdesc="Privacy-Centric Cryptographic Currency with fully encrypted transactions and anonymous block transactions. (Includes the qt-client, the headless daemon and the command-line tool.)"
provides=('darkcoin' 'darkcoind' 'darkcoin-qt' 'darkcoin-cli')
conflicts=('darkcoin' 'darkcoil' 'darkcoin-daemon-git' 'darkcoin-qt-git' 'darkcoin-cli-git')
source=("git://github.com/darkcoin/darkcoin.git")
sha512sums=('SKIP')

pkgver() {
  cd "$srcdir/$_gitname"
  git checkout "$_gitbranch" -q
  git pull -q
  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

build() {
  CXXFLAGS+=" -fPIE"
  cd "$srcdir/$_gitname"
  git checkout "$_gitbranch"
  git pull

  ./autogen.sh
  ./configure --with-incompatible-bdb --with-gui=qt5 --with-daemon --with-cli --disable-debug --disable-tests
  make
  strip ./src/qt/darkcoin-qt
  strip ./src/darkcoind
  strip ./src/darkcoin-cli
}

package() {
  install -D -m755 "$srcdir/$_gitname/src/qt/darkcoin-qt" "$pkgdir/usr/bin/darkcoin-qt"
  install -D -m755 "$srcdir/$_gitname/src/darkcoind" "$pkgdir/usr/bin/darkcoind"
  install -D -m755 "$srcdir/$_gitname/src/darkcoin-cli" "$pkgdir/usr/bin/darkcoin-cli"
  install -D -m644 "$srcdir/$_gitname/COPYING" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -D -m644 "$srcdir/$_gitname/share/pixmaps/darkcoin128.png" "$pkgdir/usr/share/pixmaps/darkcoin128.png"
  install -D -m644 "$srcdir/$_gitname/contrib/debian/darkcoin-qt.desktop" "$pkgdir/usr/share/applications/darkcoin-qt.desktop"
}
