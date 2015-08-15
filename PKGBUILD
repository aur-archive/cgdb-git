# Maintainer: J. W. Birdsong <jwbirdsong AT gmail DOT com>

pkgname=cgdb-git
pkgver=20120925
pkgrel=1
pkgdesc="Curses-based interface to the GNU Debugger"
arch=('i686' 'x86_64')
url="http://cgdb.sourceforge.net/" 
license=('GPL')
depends=('readline>=5.1' 'ncurses' 'gdb' 'help2man' )
provides=(cgdb)
conflicts=('cgdb')

#_gitroot="https://github.com/cgdb/cgdb.github.com.git"
_gitroot="git://github.com/cgdb/cgdb.git"
_gitname="cgdb"

build() {
  cd "${srcdir}"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  buillddir="${srcdir}/$_gitname-build"
  rm -rf "${buillddir}"
  git clone "$srcdir/$_gitname"  ${buillddir}
  cd "${buillddir}"

  ./autogen.sh
  ./configure --prefix=/usr 

  makeopts="PREFIX=/usr DESTDIR="${pkgdir}""
  make ${makeopts}
  make ${makeopts} install

}

# vim:set ts=2 sw=2 et:

