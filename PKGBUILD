# Maintainer: Andreas Radke <andyrtr at archlinux.org>
# Committer: Judd Vinet <jvinet@zeroflux.org>
pkgname=gnupg
pkgver=1.4.11
pkgrel=3
pkgdesc="GNU Privacy Guard - a PGP replacement tool"
arch=('i686' 'x86_64')
license=('GPL3')
depends=('zlib' 'bzip2' 'libldap>=2.4.18' 'libusb-compat' 'curl>=7.16.2' 'readline>=6.0.00')
source=(ftp://ftp.franken.de/pub/crypt/mirror/ftp.gnupg.org/gcrypt/gnupg/$pkgname-$pkgver.tar.bz2)
install=gnupg.install
url="http://www.gnupg.org/"
md5sums=('411744e1ef8ce90b87938c4203f001f1')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr \
	--libexecdir=/usr/lib \
	--enable-noexecstack
  make
  #ln -s ${pkgname}-${pkgver}/scripts .. # seems obsolete now
}

check() {
  cd "$srcdir/$pkgname-$pkgver"
  make -k check #All 27 tests passed
}

package () {
  cd ${srcdir}/${pkgname}-${pkgver}
  make DESTDIR=${pkgdir} install
  
  # fix fileconflict with gnupg2 pkg
  rm ${pkgdir}/usr/share/man/man1/gpg-zip.1
}
