# Maintainer: cdude
# Contributor: sekret

_pkgname=surf
pkgname=$_pkgname-git
pkgver=2.1.r12.g475d746
pkgrel=1
pkgdesc="a WebKit based browser"
arch=('i686' 'x86_64')
url="http://surf.suckless.org/"
license=('custom:MIT/X')
depends=('webkit2gtk' 'gcr' 'xorg-xprop')
makedepends=('git')
optdepends=('dmenu: url bar and search'
            'tabbed: tab browsing'
            'ca-certificates: SSL verification'
            'st: default terminal for the download handler'
            'curl: default download handler'
            'mpv: default video player')
provides=("$_pkgname")
conflicts=("$_pkgname")


pkgver() {
  git describe --long --tags | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
 # cd "$_pkgname"
  for file in "${source[@]}"; do
      if [[ "$file" == "config.h" ]]; then
          # add config.h if present in source array
          cp "$srcdir/$file" .
      elif [[ "$file" == *.diff || "$file" == *.patch ]]; then
          # add all patches present in source array
          patch -Np1 < "$srcdir/$(basename ${file})"
      fi
   done
}

build() {
  cd ..
  make PREFIX=/usr DESTDIR="$pkgdir"
}

package() {
  cd ..
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
