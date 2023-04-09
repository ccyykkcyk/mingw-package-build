# Maintainer: ccyykkcyk <https://github.com/ccyykkcyk>

_realname=qbittorrent
pkgbase=mingw-w64-${_realname}
pkgname=${MINGW_PACKAGE_PREFIX}-${_realname}
pkgver=4.5.2
pkgrel=1
pkgdesc="An advanced BitTorrent client programmed in C++, based on Qt toolkit and libtorrent-rasterbar (mingw-w64)"
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32' 'clangarm64')
url="https://qbittorrent.org/"
license=('spdx:GPL-2.0-or-later')
depends=("${MINGW_PACKAGE_PREFIX}-boost"
         "${MINGW_PACKAGE_PREFIX}-libtorrent-rasterbar"
         "${MINGW_PACKAGE_PREFIX}-qt6-base"
         "${MINGW_PACKAGE_PREFIX}-qt6-svg"
         "${MINGW_PACKAGE_PREFIX}-zlib")
makedepends=("git"
             "${MINGW_PACKAGE_PREFIX}-cmake"
             "${MINGW_PACKAGE_PREFIX}-ninja"
             "${MINGW_PACKAGE_PREFIX}-qt6-tools")
optdepends=("${MINGW_PACKAGE_PREFIX}-python: needed for torrent search tab")
# provides=("${MINGW_PACKAGE_PREFIX}-${_realname}")
# conflicts=("${MINGW_PACKAGE_PREFIX}-${_realname}")
source=("https://github.com/qbittorrent/qBittorrent/archive/refs/tags/release-${pkgver}.tar.gz")
sha256sums=('0a3c11296b1daa6e6dd57ebb8426e0388ba7db613e54a758b201648b69702dd4')


prepare() {
  cd "${srcdir}/${_realname}-release-${pkgver}"

  # prepare env for msys2-mingw
  sed \
    -i \
    -e 's/NTDDI_VERSION/#NTDDI_VERSION/g' \
    -e 's/_WIN32_WINNT/#_WIN32_WINNT/g' \
    -e 's/_WIN32_IE/#_WIN32_IE/g' \
    "cmake/Modules/MacroQbtCommonConfig.cmake"
}

build() {
  cp -rf ${_realname}-release-${pkgver} build-${MSYSTEM} && cd ${srcdir}/build-${MSYSTEM}

  MSYS2_ARG_CONV_EXCL="-DCMAKE_INSTALL_PREFIX=" \
    "${MINGW_PREFIX}/bin/cmake.exe" \
      -B "_build" \
      -DCMAKE_BUILD_TYPE=RelWithDebInfo \
      -DCMAKE_INSTALL_PREFIX="${MINGW_PREFIX}" \
      -DQT6=ON \
      ./
  "${MINGW_PREFIX}/bin/cmake.exe" \
    --build "_build"
}

package() {
  cd "${srcdir}/build-${MSYSTEM}"

  DESTDIR="$pkgdir" \
    "${MINGW_PREFIX}/bin/cmake.exe" \
      --install "_build"
  install -Dm644 "COPYING" -t "$pkgdir/${MINGW_PREFIX}/share/licenses/${_realname}/COPYING"

}