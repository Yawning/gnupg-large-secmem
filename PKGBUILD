# Maintainer: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname=gnupg
pkgver=2.2.5
pkgrel=2
pkgdesc='Complete and free implementation of the OpenPGP standard'
url='http://www.gnupg.org/'
license=('GPL')
arch=('x86_64')
optdepends=('libldap: gpg2keys_ldap'
            'libusb-compat: scdaemon'
            'pcsclite: scdaemon')
makedepends=('libldap' 'libusb-compat' 'pcsclite')
checkdepends=('openssh')
depends=('npth' 'libgpg-error' 'libgcrypt' 'libksba' 'libassuan'
         'pinentry' 'bzip2' 'readline' 'gnutls' 'sqlite')
validpgpkeys=('D8692123C4065DEA5E0F3AB5249B39D24F25E3B6'
              '46CC730865BB5C78EBABADCF04376F3EE0856959'
              '031EC2536E580D8EA286A9F22071B08A33BD3F06'
              'D238EA65D64C67ED4C3073F28A861B1C7EFD60D9')
source=("https://gnupg.org/ftp/gcrypt/${pkgname}/${pkgname}-${pkgver}.tar.bz2"{,.sig}
        'req_usage.patch')
sha256sums=('3fa189a32d4fb62147874eb1389047c267d9ba088f57ab521cb0df46f08aef57'
            'SKIP'
            'f8bef4891c1b9f81f305753dac7780ad4cfd56ec853502ba1d9d6400c69a518e')

install=install

conflicts=('dirmngr' 'gnupg2')
provides=('dirmngr' "gnupg2=${pkgver}")
replaces=('dirmngr' 'gnupg2')

prepare() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	sed '/noinst_SCRIPTS = gpg-zip/c sbin_SCRIPTS += gpg-zip' -i tools/Makefile.in

	# See: https://dev.gnupg.org/rGa17d2d1f690ebe5d005b4589a5fe378b6487c657
	patch -p1 -i ../req_usage.patch
}

build() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	./configure \
		--prefix=/usr \
		--sysconfdir=/etc \
		--sbindir=/usr/bin \
		--libexecdir=/usr/lib/gnupg \
		--enable-maintainer-mode \
		--enable-symcryptrun \

	make
}

check() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	make check
}

package() {
	cd "${srcdir}/${pkgname}-${pkgver}"
	make DESTDIR="${pkgdir}" install
	ln -s gpg "${pkgdir}"/usr/bin/gpg2
	ln -s gpgv "${pkgdir}"/usr/bin/gpgv2

	cd doc/examples/systemd-user
	for i in *.*; do
		install -Dm644 "$i" "${pkgdir}/usr/lib/systemd/user/$i"
	done
}
