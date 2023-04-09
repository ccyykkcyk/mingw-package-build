# Maintainer: ccyykkcyk <https://github.com/ccyykkcyk>

_realname=ntl
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=11.5.1
pkgrel=1
pkgdesc='A Library for doing Number Theory'
arch=('x86_64')
mingw_arch=('mingw64' 'ucrt64')
url='https://www.shoup.net/ntl/'
license=(LGPL)
makedepends=("${MINGW_PACKAGE_PREFIX}-autotools"
             "${MINGW_PACKAGE_PREFIX}-cc"
             "${MINGW_PACKAGE_PREFIX}-gmp")
source=(https://www.shoup.net/${_realname}/${_realname}-${pkgver}.tar.gz)
sha256sums=('210d06c31306cbc6eaf6814453c56c776d9d8e8df36d74eb306f6a523d1c6a8a')

build() {
  mkdir -p "${srcdir}/build-${MSYSTEM}" && cd "${srcdir}/${_realname}-${pkgver}/src"
  ./configure \
  DEF_PREFIX="${MINGW_PREFIX}" \
  NATIVE=off \
  CXXFLAGS="-g -O2" \
  LDFLAGS="${LDFLAGS}" \
  LIBTOOL_LINK_FLAGS=-no-undefined \
  SHARED=on

  make
}

check() {
  cd "${srcdir}/${_realname}-${pkgver}/src"

  make -k check
}

package() {
  cd "${srcdir}/${_realname}-${pkgver}/src"

  make PREFIX="${pkgdir}" install
}
