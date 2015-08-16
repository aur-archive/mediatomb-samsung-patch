# Maintainer: Peter Richard Lewis <plewis@aur.archlinux.org>
# Contributor: William Rea <sillywilly@gmail.com>
# Contributor: Nikhil Bysani <nikron@gmail.com>
# Contributor: Mika HynnÃ¤ <igheax@gmail.com>
# Contributor: Jonathan Conder <jonno.conder@gmail.com>
# Contributor : emmanuelux : i add the patch here : http://sourceforge.net/tracker/?func=detail&aid=3532724&group_id=129766&atid=715782

pkgname=mediatomb-samsung-patch
pkgver=0.12.1
pkgrel=11
pkgdesc="Free UPnP/DLNA media server"
arch=('i686' 'x86_64')
url="http://mediatomb.cc/"
license=('GPL')
depends=('file' 'curl' 'ffmpegthumbnailer' 'js' 'libexif' 'libmp4v2' 'sqlite3' 'taglib' 'libmysqlclient')
optdepends=('mysql: to store your music database in mysql')
backup=('etc/conf.d/mediatomb')
install=mediatomb.install
conflicts=(mediatomb)
source=("http://downloads.sourceforge.net/mediatomb/mediatomb-$pkgver.tar.gz"
        'mediatomb.rc'
        'mediatomb.conf'
        'gcc46.patch'
        'tonewjs.patch'
        'jsparse.patch'
        'libav_0.7_support.patch'
        'libmp4v2_191_p497.patch'
        'libavformat.patch'
        'mediatomb-urifix.patch')

build() {
  cd "$srcdir/mediatomb-$pkgver"
  patch -Np1 -i "$srcdir/gcc46.patch"
  patch -Np1 -i "$srcdir/tonewjs.patch"
  patch -Np1 -i "$srcdir/jsparse.patch"
  patch -Np1 -i "$srcdir/libav_0.7_support.patch"
  patch -Np1 -i "$srcdir/libmp4v2_191_p497.patch"
  patch -Np1 -i "$srcdir/libavformat.patch"
  patch -Np1 -i "$srcdir/mediatomb-urifix.patch"

  ./configure --prefix=/usr \
              --enable-mysql \
              --enable-libmagic \
              --enable-libjs \
              --enable-ffmpeg
  make
}

package() {
  cd "$srcdir/mediatomb-$pkgver"

  make DESTDIR="$pkgdir/" install

  install -D -m0755 "$srcdir/mediatomb.rc" "$pkgdir/etc/rc.d/mediatomb"
  install -D -m0755 "$srcdir/mediatomb.conf" "$pkgdir/etc/conf.d/mediatomb"
  install -d "$pkgdir/var/lib/mediatomb"
}
sha256sums=('31163c34a7b9d1c9735181737cb31306f29f1f2a0335fb4f53ecccf8f62f11cd'
            '1a67a1deb8a41467fe9bbf66358a255f0df97b0170a5fc3d48c1f768c8d328b9'
            'ba9753a4a380d4c717c987efec03a3c6d401d3ff93a6fced28098adbd3a44cc9'
            '0c02a20032f0c296800b1bb9644638970c2dedbc5ab7141d66a637235e9da6ce'
            '2cd8f5628c3a38b290526f008bae351b90211825f86e5959bf95f140748de574'
            'd9a3062858900d32b977f0d50d168fd7d36785b6ecc038c019e661e27f7b1c17'
            'c6523e8bf5e2da89b7475d6777ef9bffe7d089752ef2f7b27b5e39a4130fb0ff'
            'd39c2f9aab051c5447461718fd0ec72cf5982f6c920a4a985a50831f34babe84'
            '76b11706d70ed8f5e157d96ca441c90c46c42176102fcb651b4ab1102b61bfee'
            '537373654c1d7fa24e14f2e5a9c78228589411509d46fbd53bb38b87d5ee34fb')
