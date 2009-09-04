# Maintainer: Andreas Radke <andyrtr at archlinux.org>
# Committer: Judd Vinet <jvinet@zeroflux.org>
pkgname=gnupg
pkgver=1.4.10
pkgrel=1
pkgdesc="GNU Privacy Guard - a PGP replacement tool"
arch=(i686 x86_64)
license=('GPL3')
depends=('zlib' 'bzip2' 'libldap' 'libusb' 'curl>=7.16.2' 'readline>=6.0.00')
source=(ftp://ftp.franken.de/pub/crypt/mirror/ftp.gnupg.org/gcrypt/gnupg/$pkgname-$pkgver.tar.bz2)
install=gnupg.install
url="http://www.gnupg.org/"
md5sums=('dcf7ed712997888d616e029637bfc303')

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/usr --libexecdir=/usr/lib # docdir can't be set properly
  make || return 1
  ln -s ${pkgname}-${pkgver}/scripts ..
  make DESTDIR=${pkgdir} install || return 1
  
  # fix fileconflict with gnupg2 pkg
  rm ${pkgdir}/usr/share/man/man1/gpg-zip.1
}
