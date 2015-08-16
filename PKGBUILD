# Contributor: Adria Arrufat (archdria) <swiftscythe at gmail.com>
pkgname=kmess-telepathy-git
pkgver=20120409
pkgrel=1
pkgdesc="A full-featured IM Client - GIT development version using telepathy"
arch=('i686' 'x86_64')
url="http://www.kmess.org/"
license=('GPL')
depends=('qt' 'libxss' 'telepathy-qt>0.9' 'telepathy-mission-control')
makedepends=('git' 'cmake' 'automoc4' 'docbook-xsl')
install=$pkgname.install

_gitroot="git://gitorious.org/kmess/kmesstelepathy.git"
_gitname="kmesstelepathy-git"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf ${srcdir}/build
  mkdir ${srcdir}/build
  cd ${srcdir}/build

  cmake ../$_gitname \
    -DCMAKE_INSTALL_PREFIX=`kde4-config --prefix` \
    -DCMAKE_BUILD_TYPE=Release
  make || return 1
}

package() {
  cd ${srcdir}/build
  make DESTDIR=${pkgdir} install || return 1
} 
