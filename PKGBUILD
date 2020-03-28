## $Id$
# Contributor: Alexey Andreyev <aa13q@ya.ru>
# Maintainer: James Kittsmiller (AJSlye) <james@nulogicsystems.com>

pkgname=sailfish-user-managerd-git
_srcname=sailfish-user-managerd
pkgver=0.2.0.r0.g317f9b7
pkgrel=1
pkgdesc="Sailfish user manager daemon"
arch=('x86_64' 'aarch64')
url="https://github.com/sailfishos/user-managerd"
license=('BSD')
depends=('qt5-base')
makedepends=('git' 'libuser' 'sailfish-access-control-git')
optdepends=()
provides=("${_srcname}")
conflicts=()
source=(
  "${pkgname}::git+${url}.git")
sha256sums=('SKIP')

pkgver() {
  cd "${srcdir}/${pkgname}"
  ( set -o pipefail
    git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  ) 2>/dev/null
}

build() {
  cd "${srcdir}/${pkgname}"
  mkdir -p build
  cd build
  qmake ..
  make
}

package() {
  cd "${srcdir}/${pkgname}"
  cd build
  make INSTALL_ROOT="${pkgdir}" install
  cd "${pkgdir}"
  # TODO: specify via qmake/make veriable
  mv lib/systemd usr/lib
  rm -rf lib
}
