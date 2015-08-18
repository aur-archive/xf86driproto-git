# Maintainer: Federico Cinelli <cinelli.federico@gmail.com>

pkgname=xf86driproto-git
pkgver=20130316
pkgrel=1
pkgdesc="X11 DRI extension wire protocol"
license=('custom')
url="http://xorg.freedesktop.org/"
arch=('any')
provides=('xf86driproto' 'xf86driproto-git')
replaces=("xf86driproto")
conflicts=("xf86driproto")
depends=("xorg-util-macros")

_gitroot="git://git.freedesktop.org/git/xorg/proto/xf86driproto"
_gitname="xf86driproto"

build() {
  cd ${srcdir}
  msg "Connecting to git.freedesktop.org GIT server...."

  if [[ -d $_gitname ]] ; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  
  ./autogen.sh --prefix=/usr
  make
}

package() {
  make -C "$srcdir/$_gitname-build" DESTDIR="$pkgdir" install
}
