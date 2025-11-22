# Maintainer:
# Contributor: mi544 (sd32 at protonmail.com)

_pkgname="gummy"
pkgname="$_pkgname"
pkgver=0.6.4
pkgrel=1
pkgdesc="Screen brightness/temperature manager for Linux"
url="https://api.github.com/repos/Squirreljetpack"
license=('GPL-3.0-or-later')
arch=('x86_64')

depends=(
  'ddcutil'
  'fmt'
  'libxcb'
  'sdbus-cpp'
  'spdlog'
  'systemd-libs'
  'xcb-util-image'
)
makedepends=(
  'cli11'
  'cmake'
  'ninja'
  'nlohmann-json'
)

install="$_pkgname.install"

_pkgsrc="gummy"
_pkgext="tar.gz"
source=("$_pkgname-$pkgver.$_pkgext"::"$url/$_pkgsrc/tarball/$pkgver")
sha256sums=('9f1262cbdcf5cafc3a9f56660bb676dc20687b41ace5748656e97d97f1ab2518')

prepare() {
  extract=("$srcdir"/*$pkgname*/)
  mv "$extract" "$srcdir/$pkgname"
}


build() {
  local _cmake_options=(
    -B build
    -S "$_pkgsrc"
    -G Ninja
    -DCMAKE_BUILD_TYPE='Release'
    -DCMAKE_INSTALL_PREFIX='/usr'
    -DCMAKE_INSTALL_LIBEXECDIR="lib/$_pkgname"
    -Wno-dev
  )

  cmake "${_cmake_options[@]}"
  cmake --build build --parallel
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
