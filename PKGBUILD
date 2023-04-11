# Maintainer: Naveen M K <naveen521kk@gmail.com>

_realname=starship
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
pkgver=1.14.0
pkgrel=1
pkgdesc="The cross-shell prompt for astronauts (mingw-w64)"
arch=('any')
mingw_arch=('mingw32' 'mingw64' 'ucrt64' 'clang64' 'clang32')
url="https://starship.rs"
license=('spdx:ISC')
depends=("${MINGW_PACKAGE_PREFIX}-libgit2")
makedepends=("${MINGW_PACKAGE_PREFIX}-rust"
             "${MINGW_PACKAGE_PREFIX}-cmake")
options=('staticlibs' 'strip')
source=("${_realname}-${pkgver}.tar.gz::https://github.com/starship/starship/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('f72f37b7f7a908be70b6b1435a1e7e44ef66710d7c57e290d3ac1107b9b4031a')
noextract=("${_realname}-${pkgver}.tar.gz")

prepare() {
  tar -xzf "${srcdir}"/${_realname}-${pkgver}.tar.gz -C ${srcdir} || true
  cp -r ${_realname}-${pkgver} build-${MSYSTEM}
  ${MINGW_PREFIX}/bin/cargo fetch \
  --locked \
  --manifest-path build-${MSYSTEM}/Cargo.toml
}

build() {
  export WINAPI_NO_BUNDLED_LIBRARIES=1
  ${MINGW_PREFIX}/bin/cargo build \
  --release \
  --frozen \
  --manifest-path build-${MSYSTEM}/Cargo.toml
}

package() {
  ${MINGW_PREFIX}/bin/cargo install \
  --frozen \
  --offline \
  --no-track \
  --path build-${MSYSTEM} \
  --root ${pkgdir}${MINGW_PREFIX}

  install -Dm 644 build-${MSYSTEM}/LICENSE -t "${pkgdir}${MINGW_PREFIX}"/share/licenses/starship/
  install -dm 755 "${pkgdir}${MINGW_PREFIX}"/share/{bash-completion/completions,fish/vendor_completions.d,zsh/site-functions}/
  ./build-${MSYSTEM}/target/release/starship completions bash >"${pkgdir}${MINGW_PREFIX}"/share/bash-completion/completions/starship
  ./build-${MSYSTEM}/target/release/starship completions fish >"${pkgdir}${MINGW_PREFIX}"/share/fish/vendor_completions.d/starship.fish
  ./build-${MSYSTEM}/target/release/starship completions zsh >"${pkgdir}${MINGW_PREFIX}"/share/zsh/site-functions/_starship
}