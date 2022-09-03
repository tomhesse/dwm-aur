pkgname=dwm
pkgver=6.3
pkgrel=4
pkgdesc="A dynamic window manager for X"
url="https://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama' 'libxft' 'freetype2' 'ttf-hack')
source=(dwm.desktop
        https://dl.suckless.org/dwm/dwm-$pkgver.tar.gz
        https://raw.githubusercontent.com/tomhesse/dwm-patches/main/dwm-notitlecolor-6.3.diff
        https://dwm.suckless.org/patches/ru_gaps/dwm-ru_gaps-6.3.diff
        config.h)
sha256sums=('28c8d5bcaca83b7e945d6f52e91d3941f6d67e489d8a8484cc20546a8149bbf4'
            'badaa028529b1fba1fd7f9a84f3b64f31190466c858011b53e2f7b70c6a3078d'
            '45ffab26cf29e993f4ae5efd7262c6b65ccb7f12daaba2a33a86f6eb50fd0391'
            'bdbfe23f2ca8bcc04ed2e0f08d0389aa3f7874b236177d6a81432ac8d5e56d60'
            '3c16197a3a70640848b7f99aceefc155baff13ecd832f572674649a4608e2ee4')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h

  for patch in "$srcdir"/*.diff; do
    if [ -f "$patch" ]; then
      echo "Applying $(basename "$patch")"
      patch -p1 --quiet < "$patch"
    fi
  done
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
  install -Dm644 "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
