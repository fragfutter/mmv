# Maintainer: Cedric Girard <girard.cedric@gmail.com>
# Contributor: blue_lizard lizard@blue.dyn-o-saur.com

pkgname=mmv
pkgver=1.01b.orig
pkgrel=4
pkgdesc="multiple move files"
source=(http://ftp.de.debian.org/debian/pool/main/m/mmv/mmv_1.01b.orig.tar.gz http://ftp.de.debian.org/debian/pool/main/m/mmv/mmv_1.01b-19.debian.tar.xz)
md5sums=('1b2135ab2f17bdfa9e08debbb3c46ad8' '5952faa99a610afdbba73d20d68c6d0f')

url="http://linux.maruhn.com/sec/mmv.html"
license=('GPL')
install=$pkgname.install
arch=('i686' 'x86_64')

prepare() {
  tar xJvf mmv_1.01b-19.debian.tar.xz 
  cd "${srcdir}/$pkgname-$pkgver"
  for i in $(cat ../debian/patches/series); do
    echo $i
    patch -p1 < ../debian/patches/$i
  done
  sed -i -e "s/LDFLAGS.\s=-s -N/LDFLAGS	=-s/g" Makefile
  sed -i 's!/usr/man!/usr/share/man!' Makefile
}

build() {
  cd "${srcdir}/$pkgname-$pkgver"
  make
}

package(){
  cd "${srcdir}/$pkgname-$pkgver"
  mkdir -p "${pkgdir}/usr/bin"
  mkdir -p "${pkgdir}/usr/share/man/man1"
  make DESTDIR="${pkgdir}" install
  chmod 644 "${pkgdir}/usr/share/man/man1/mmv.1"
  cd "${pkgdir}/usr/bin"
  ln -s mmv mcp
  ln -s mmv mad
  ln -s mmv mln
  cd "${pkgdir}/usr/share/man/man1/"
  ln -s mmv.1 mcp.1
  ln -s mmv.1 mad.1
  ln -s mmv.1 mln.1
}
