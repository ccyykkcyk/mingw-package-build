# Maintainer: ccyykkcyk <https://github.com/ccyykkcyk>

_realname=gf2x
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=1.3.0
pkgrel=1
pkgdesc='A library for multiplying polynomials over the binary field'
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
url='https://gitlab.inria.fr/gf2x/gf2x'
license=(LGPL)
makedepends=("${MINGW_PACKAGE_PREFIX}-autotools"
             "${MINGW_PACKAGE_PREFIX}-cc")
source=(https://gitlab.inria.fr/gf2x/gf2x/uploads/c46b1047ba841c20d1225ae73ad6e4cd/${_realname}-${pkgver}.tar.gz)
sha256sums=('9472cd651972a1de38e3c4c47697a86e0ecf19d7d33454d4bc2a62bc85841b59')

build() {
  mkdir -p "${srcdir}/build-${MSYSTEM}" && cd "${srcdir}/build-${MSYSTEM}"
  ../"${_realname}-${pkgver}"/configure \
  --prefix="${MINGW_PREFIX}" \
  --build="${MINGW_CHOST}" \
  --host="${MINGW_CHOST}" \
  --target="${MINGW_CHOST}"

  make
}

check() {
  cd "${srcdir}/build-${MSYSTEM}"

  make -k check
}

package() {
  cd "${srcdir}/build-${MSYSTEM}"

  make prefix="${pkgdir}" install
}
