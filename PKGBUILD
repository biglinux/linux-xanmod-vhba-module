# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard@manjaro.org>

# Arch credits:
# Ray Rashif <schiv@archlinux.org>
# Mateusz Herych <heniekk@gmail.com>
# Charles Lindsay <charles@chaoslizard.org>

_linuxprefix=linux-xanmod

_module=vhba-module
pkgname="${_linuxprefix}-${_module}"
pkgver=20211218
pkgrel=67910
pkgdesc="Kernel module that emulates SCSI devices"
arch=('x86_64')
url="https://cdemu.sourceforge.io/"
license=('GPL-2.0-or-later')
depends=("${_linuxprefix}")
makedepends=("${_linuxprefix}-headers")
provides=("${_module}=$pkgver" "VHBA-MODULE")
groups=("${_linuxprefix}-extramodules")
source=("http://downloads.sourceforge.net/cdemu/${_module}-$pkgver.tar.xz")
sha256sums=('72c5a8c1c452805e4cef8cafefcecc2d25ce197ae4c67383082802e5adcd77b6')

build() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"

  cd "${_module}-$pkgver"
  make KERNELRELEASE="${_kernver}"
}

package() {
  _kernver="$(cat /usr/src/${_linuxprefix}/version)"

  cd "${_module}-$pkgver"
  install -Dm644 *.ko -t "$pkgdir/usr/lib/modules/${_kernver}/extramodules/"

  find "$pkgdir" -name '*.ko' -exec strip --strip-debug {} +
  find "$pkgdir" -name '*.ko' -exec xz {} +
}
