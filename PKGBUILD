# Maintainer: David Runge <dvzrv@archlinux.org>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Lukas Fleischer <lfleischer@archlinux.org>
# Contributor: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Andreas Radke <andyrtr@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname=gnupg
pkgver=2.2.41
pkgrel=2
pkgdesc='Complete and free implementation of the OpenPGP standard'
arch=(x86_64)
url='https://www.gnupg.org/'
license=(
  BSD-2-Clause
  BSD-3-Clause
  CC0-1.0
  GPL-2.0-or-later
  GPL-3.0-or-later
  LGPL-2.1-or-later
  'LGPL-3.0-or-later OR GPL-2.0-or-later'
  MIT
  Unicode-TOU
)
depends=(
  bzip2 libbz2.so
  glibc
  gnutls
  libgcrypt
  libgpg-error
  libksba
  libassuan libassuan.so
  libldap
  libusb
  npth libnpth.so
  pinentry
  readline libreadline.so
  sh
  sqlite
  zlib
)
makedepends=(pcsclite)
checkdepends=(openssh)
optdepends=(
  'pcsclite: for using scdaemon not with the gnupg internal card driver'
)
install=$pkgname.install
source=(
  https://gnupg.org/ftp/gcrypt/$pkgname/$pkgname-$pkgver.tar.bz2{,.sig}
  dirmngr.{service,socket}
  gpg-agent{,-{browser,extra,ssh}}.socket
  gpg-agent.service
  drop-import-clean.patch
  avoid-beta-warning.patch
)
sha256sums=('13f3291007a5e8546fcb7bc0c6610ce44aaa9b3995059d4f8145ba09fd5be3e1'
            'SKIP'
            '80a3a80f9f1f337da555a6838483e1baca44cde8a8a3d8c4ba7743626304b981'
            '8374255ce93a3c343019ab425963bcbc41982ea89e669d1ad1df0aa7be810de1'
            '81e9dd05cbf3b8406367258eae6ef67ff97f270301bf50b52742647c515c8304'
            '1cf9821b3bf4efaf4da2fd52ceb70d254dc4f6c545603f9045de716ef6aabf2d'
            'f0094f67586cbcda17fd0d780e3e73d6dbaa479ac84715ba941531f83f6ecfe9'
            'ffa0191fad52712732f8b24d7d570c1d19a7803e59d30088797b76e252f65858'
            '8ea489a57edb0db9394bf2d6c0ec62205f881bb54efb919e4870209c7db01aa7'
            '02d375f0045f56f7dd82bacdb5ce559afd52ded8b75f6b2673c39ec666e81abc'
            '22fdf9490fad477f225e731c417867d9e7571ac654944e8be63a1fbaccd5c62d')
b2sums=('0be2965a646a8636a127f89329030860908b0bbc447381782527459aed85f5276c29e7a2c89f87cb715407d9f1aabbf3ae1765073764d05e422035e8d5962569'
        'SKIP'
        '7a3af856305eb4b00929aaf029dd4e5c84376df4f30add76976b9b058addf6fc4d8c39335fc83d11493ea9d8a40f0510dbac8572b99a8c8b9b3a4eca8e585774'
        'ee51a4702715f5ec2629ff42eeba8630010da8a67545d1e53961e710de5faf197708e55d2d55796917a134ca2a76b1d6c88a8f7756d0706e0cbc33b605f52d86'
        '129ecd9df3f00ed28f494f914483645e9aeaa1d6812c762ded60582c0a3f66b215731d4415ea5c017aa5ce97448faa5b93dbcb3793a82643d6ed160cc62f4ea4'
        'bf5daa4a33daae716a1d7743470dae618151e14ab7bb5d99138f880a908fac57dbb517b78d92c81ecf4532c25366cd32f7acc0e33a711ccde830fbc208726e69'
        'ffc8ea3c7875b195720ad238742a726b4b7be0bb8f2f8927358d259202f22b5e32f9ad23a4c66da85e25f36544770c29725be6d99256b685427b94d814e29196'
        '9dd03f808af45752a01ccbcfec3f3cb39f1a720088e21aa8a19c2ceec3876b3a8b950c1c154203d0adc208fed8ae07a26c8cd59d783e32eb1294a3a340bedad4'
        'ad71d7fab2a92a8da454c34884b5724e94adc0925a7f97f062fb7b78ed3ec87e5babb6383e755c943afd16bf61789ba83455dc2baf82ce248c1c4622ff87e364'
        'd598015e7f27b27840667d1656c083b4ad85d6acdd312e9929854067313a5f28415ee7eecf4d84a4b8da0385b667aaa01a9743461f5c785402a56c238274e376'
        '7ea069e81e2d91a3154bcb62516b4b599f34596de277f95ad1ccaba73869c4f84f94f063b65026ba0bc8a72c0fd8e8e182b82346964f67ea78166b6399c923c5')
validpgpkeys=(
  '5B80C5754298F0CB55D8ED6ABCEF7E294B092E28' # Andre Heinecke (Release Signing Key)
  '6DAA6E64A76D2840571B4902528897B826403ADA' # Werner Koch (dist signing 2020)
  'AC8E115BF73E2D8D47FA9908E98E9B2D19C6C8BD' # Niibe Yutaka (GnuPG Release Key)
  '02F38DFF731FF97CB039A1DA549E695E905BA208' # GnuPG.com (Release Signing Key 2021)
)

prepare() {
  cd $pkgname-$pkgver

  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  # improve reproducibility
  rm doc/gnupg.info*

  ./autogen.sh
}

build() {
  local configure_options=(
    --enable-maintainer-mode
    --libexecdir=/usr/lib/gnupg
    --prefix=/usr
    --sbindir=/usr/bin
    --sysconfdir=/etc
  )

  cd $pkgname-$pkgver
  ./configure "${configure_options[@]}"
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
  local units=({dirmngr,gpg-agent{,-{browser,extra,ssh}}}.socket)
  local socket_target_dir="$pkgdir/usr/lib/systemd/user/sockets.target.wants/"
  local unit

  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  ln -s gpg "$pkgdir"/usr/bin/gpg2
  ln -s gpgv "$pkgdir"/usr/bin/gpgv2

  install -Dm 644 ../*.{service,socket} -t "$pkgdir/usr/lib/systemd/user/"
  install -Dm 644 COPYING.{CC0,other} -t "$pkgdir/usr/share/licenses/$pkgname/"

  install -vdm 755 "$socket_target_dir"
  for unit in "${units[@]}"; do
    ln -sv "../$unit" "$socket_target_dir$unit"
  done
}

# vim: ts=2 sw=2 et:
