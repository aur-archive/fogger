# Maintainer: Ran Jiao <ranjiao@gmail.com>

pkgname=fogger
pkgver=221
pkgrel=2
pkgdesc="bzr version of fogger web app to desktop app, patched for archlinux"
arch=('i686' 'x86_64')
url="http://launchpad.net/fogger"
license=('GPL')
depends=('desktop-file-utils' 'python2-beautifulsoup3')
makedepends=('bzr' 'python2-distutils-extra' 'python-requests')
conflicts=('fogger')
replaces=('fogger')
install=fogger-bzr.install
sha256sums=()

_bzrtrunk=lp:~ranjiao/fogger/fogger
_bzrmod=fogger

build() {
  cd "$srcdir"
  if [ -d ${_bzrmod} ]; then
  bzr up ${_bzrmod}
    msg "The local files are updated."
  else
    bzr co ${_bzrtrunk} ${_bzrmod}
  fi
  msg "Bazaar checkout done or server timeout"
  msg "Starting make..."
  if [[ -d ${srcdir}/build ]]; then
    msg "Cleaning the previous build directory..."
    rm -rf ${srcdir}/build
  fi
  bzr clone ${srcdir}/${_bzrmod} ${srcdir}/build
  cd ${srcdir}/build
  python2 setup.py build
}

package() {
  cd ${srcdir}/build
  mkdir -p ${pkgdir}/usr/share/icons
  cp ${srcdir}/fogger/data/media/fogger.svg ${pkgdir}/usr/share/icons
  python2 setup.py install --root=$pkgdir
}

# vim:set ts=2 sw=2 et:
