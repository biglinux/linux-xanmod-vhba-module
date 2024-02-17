# Maintainer: Bernhard Landauer <bernhard@manjaro.org>
# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Archlinux credits:
# Ray Rashif <schiv@archlinux.org>
# Mateusz Herych <heniekk@gmail.com>
# Charles Lindsay <charles@chaoslizard.org>

_linuxprefix=linux-xanmod
_kernver="$(cat /usr/src/${_linuxprefix}/version)"
pkgname=$_linuxprefix-vhba-module
_pkgname=vhba-module
pkgver=20211218
pkgrel=67510
pkgdesc="Kernel module that emulates SCSI devices"
arch=('x86_64')
url="http://cdemu.sourceforge.net/"
license=('GPL')
depends=("$_linuxprefix")
makedepends=("$_linuxprefix-headers")
provides=("$_pkgname=$pkgver" "VHBA-MODULE")
groups=("$_linuxprefix-extramodules")
source=("http://downloads.sourceforge.net/cdemu/$_pkgname-$pkgver.tar.xz"
        '60-vhba.rules')
sha256sums=('72c5a8c1c452805e4cef8cafefcecc2d25ce197ae4c67383082802e5adcd77b6'
            '3052cb1cadbdf4bfb0b588bb8ed80691940d8dd63dc5502943d597eaf9f40c3b')

prepare() {
  cd "$_pkgname-$pkgver"

  local src
  for src in "${source[@]}"; do
      src="${src%%::*}"
      src="${src##*/}"
      [[ $src = *.patch ]] || continue
      msg2 "Applying patch: $src..."
      patch -Np1 < "../$src"
  done
}

build() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"

  cd "$_pkgname-$pkgver"
  make -j1 KDIR=/usr/lib/modules/${_kernver}/build
}

package() {
  cd "$_pkgname-$pkgver"
  install -D vhba.ko "$pkgdir/usr/lib/modules/${_kernver}/extramodules/vhba.ko"
  find "$pkgdir" -name '*.ko' -exec gzip -9 {} \;
}
