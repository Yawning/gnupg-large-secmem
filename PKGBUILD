# Maintainer: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname=gnupg
pkgver=2.0.19
pkgrel=3
pkgdesc='Complete and free implementation of the OpenPGP standard'
url='http://www.gnupg.org/'
license=('GPL')
arch=('i686' 'x86_64')
optdepends=('curl: gpg2keys_curl'
            'libldap: gpg2keys_ldap'
            'libusb-compat: scdaemon')
makedepends=('curl' 'libldap' 'libusb-compat')
depends=('bzip2' 'libksba' 'libgcrypt' 'pth' 'libassuan' 'readline' 'pinentry' 'dirmngr')
source=("ftp://ftp.gnupg.org/gcrypt/${pkgname}/${pkgname}-${pkgver}.tar.bz2"{,.sig}
        'protect-tool-env.patch')
sha1sums=('190c09e6688f688fb0a5cf884d01e240d957ac1f'
          'f6e6830610a8629b0aad69d789373bf8ca481733'
          '2ec97ba55ae47ff0d63bc813b8c64cb79cef11db')

install=install

conflicts=('gnupg2')
provides=("gnupg2=${pkgver}")
replaces=('gnupg2')

build() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	patch -p1 -i ../protect-tool-env.patch # FS#31900
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
	ln -s gpg2 "${pkgdir}"/usr/bin/gpgv
	ln -s gpg2.1.gz "${pkgdir}"/usr/share/man/man1/gpg.1.gz
	rm "${pkgdir}/usr/share/gnupg/com-certs.pem" # FS#33059
}
