# Maintainer: Konstantin Podsvirov <konstantin@podsvirov.pro>

_realname=asio
pkgbase=mingw-w64-${_realname}
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=1.26.0
pkgrel=1
pkgdesc='Cross-platform C++ library for ASynchronous network I/O (mingw-w64)'
url='https://think-async.com/Asio/'
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
license=('spdx:BSL-1.0')
makedepends=("${MINGW_PACKAGE_PREFIX}-cc"
             "${MINGW_PACKAGE_PREFIX}-boost"
             "${MINGW_PACKAGE_PREFIX}-autotools"
             "${MINGW_PACKAGE_PREFIX}-openssl")
_realver=${pkgver//./-}
_realpath=${_realname}-${_realname}-${_realver}
source=("${_realpath}.tar.gz::https://github.com/chriskohlhoff/${_realname}/archive/${_realname}-${_realver}.tar.gz")
sha256sums=('935583f86825b7b212479277d03543e0f419a55677fa8cb73a79a927b858a72d')

prepare() {
  cd ${srcdir}/${_realpath}/${_realname}/

  autoreconf -fiv
}

build() {
  cd ${srcdir}/${_realpath}/${_realname}/

  CPPFLAGS+=" -D_WIN32_WINNT=0x601" \
  ./configure \
    --prefix=${MINGW_PREFIX} \
    --build=${MINGW_CHOST} \
    --host=${MINGW_CHOST} \
    --with-boost=yes \
    --with-openssl=yes

  make
}

check() {
  cd ${srcdir}/${_realpath}/${_realname}/
  make check
}

package() {
  cd ${srcdir}/${_realpath}/${_realname}/
  make DESTDIR=${pkgdir} install

  install -Dm 644 COPYING LICENSE_1_0.txt -t "${pkgdir}${MINGW_PREFIX}/share/licenses/${_realname}"
}