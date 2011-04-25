# Maintainer: Juho Rutila <juho.rutila@gmail.com>
pkgname=akonadi-facebook-git
pkgver=20110425
pkgrel=1
pkgdesc="Facebook support in KDEPIM"
arch=('i686' 'x86_64')
url="https://thomasmcguire.wordpress.com/2011/02/27/facebook-support-in-kdepim/"
license=('unknown')
depends=('qjson' 'boost' 'libxslt')
makedepends=('git')
provides=('akonadi-facebook')

_gitroot="git://anongit.kde.org/akonadi-facebook"
_gitname="akonadi-facebook"

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

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  #
  # BUILD HERE
  #
  cmake -DCMAKE_INSTALL_PREFIX="/usr" .
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
} 
