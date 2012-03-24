# Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname=gnupg
pkgver=2.0.18
pkgrel=1
pkgdesc='Complete and free implementation of the OpenPGP standard'
url='http://www.gnupg.org/'
license=('GPL')
arch=('i686' 'x86_64')
optdepends=('curl: gpg2keys_curl'
            'libldap: gpg2keys_ldap'
            'libusb-compat: scdaemon'
            'texinfo: documentation')
makedepends=('curl' 'libldap' 'libusb-compat' 'texinfo')
depends=('bzip2' 'libksba' 'libgcrypt' 'pth' 'libassuan' 'readline' 'pinentry' 'dirmngr')
install=${pkgname}.install
source=(ftp://ftp.gnupg.org/gcrypt/gnupg/gnupg-$pkgver.tar.bz2{,.sig})
sha1sums=('5ec2f718760cc3121970a140aeea004b64545c46'
          'c1b15a6c204434081e2bd8249dde233b6c88c4d0')

conflicts=('gnupg2')
provides=("gnupg2=${pkgver}")
replaces=('gnupg2')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr --libexecdir=/usr/lib/gnupg
  make
}

check() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make check
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  ln -s gpg2 "${pkgdir}"/usr/bin/gpg
}
