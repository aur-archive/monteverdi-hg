# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Argyros Argyridis <arargyridis@gmail.com>
pkgname=monteverdi-hg
pkgver=2113
pkgrel=1
pkgdesc="A remote sensing application based on Orfeo Toolbox"
arch=(x86_64)
url="http://www.orfeo-toolbox.org/otb/monteverdi.html"
license=('CeCILL')
groups=()
depends=('orfeo-toolbox-hg')
makedepends=()
optdepends=()
provides=(monteverdi-${pkgname%-hg})
conflicts=(monteverdi--${pkgname%-hg})
replaces=(monteverdi)
backup=()
options=()
install=
changelog=
source=(otb.conf)
md5sums=(73a3855c87c2bcabde62a68009ceb030)

_hgroot=http://hg.orfeo-toolbox.org/
_hgrepo=Monteverdi
build() {

  cd $srcdir/
  msg "connecting to server..."

  if [ ! -d "$srcdir/Monteverdi" ]; then
    hg clone ${_hgroot}/${_hgrepo}
  else

    cd $srcdir/$_hgrepo
    hg pull -u
    hg update
    cd ..
  fi

  #msg "checking done or server timeout occurerror while loading shared libraries: libfltk.so.9: cannot open shared object file: No such file or directory    ed"
  
  msg "starting make..."
  rm -rf build/
  mkdir build/
  cd build
  ls -l

  cmake ../Monteverdi -DCMAKE_INSTALL_PREFIX=/usr \

  make -j9
}

package() {

  cd "$srcdir/"build
  make DESTDIR="$pkgdir" install
  
  mkdir  -m755 -p "$pkgdir"/etc/ld.so.conf.d/
  install -D -m644 "$srcdir"/otb.conf "$pkgdir"/etc/ld.so.conf.d/
  
}
