# Maintainer: Leo von Klenze <devel@leo.von-klenze.de>
pkgname=opendias
pkgver=0.9.5
pkgrel=2
pkgdesc="The openDias project is an Open Source offering, to bring a professional document scanning and storage utility for the home user"
arch=('any')
url="http://opendias.essentialcollections.co.uk"
license=('unknown')
depends=('libmicrohttpd' 'sqlite' 'uuid' 'openssl' 'phash')
makedepends=('automake' 'tesseract')
optdepends=('sane' 'leptonica' 'magic' 'xml2' 'zziplib' 'poppler' 'tesseract-data-eng')
install=opendias.install
backup=("etc/opendias/opendias.conf")
source=("https://github.com/clearscene/$pkgname/archive/$pkgver.tar.gz"
        "opendias.patch"
        "opendias.conf"
        "opendias.service")
md5sums=('b18515b38c5d43704c5c39cda1935fd8'
         'eea2d8070450ae0e92ba9339d49b4c63'
         '78739781acda7be77406a2f3aa9f280f'
         '43f1587af58c1581789f401551577ecd')

prepare() {
       cd "$srcdir/$pkgname-$pkgver"
       patch -p1 < "$srcdir/opendias.patch"
}

build() {
	cd "$srcdir/$pkgname-$pkgver"
	autoreconf -iv
	./configure --prefix=/usr --enable-force_var_at_root
	make
}

package() {
	cd "$srcdir/$pkgname-$pkgver"
	make DESTDIR="$pkgdir/" install
  
        install -D "$srcdir"/opendias.service "$pkgdir"/usr/lib/systemd/system/opendias.service
        install -D "$srcdir"/opendias.conf "$pkgdir"/usr/lib/tmpfiles.d/opendias.conf  

        install -d "$pkgdir/var/log/opendias"
        install -d "$pkgdir/etc/opendias"
        echo "/srv/opendias" > "$pkgdir/etc/opendias/opendias.conf"
}

