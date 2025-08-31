pkgname=cmake
pkgver=4.1.0
pkgrel=1
pkgdesc="A cross-platform open-source make system"
arch=('x86_64')
url="https://www.cmake.org/"
license=('custom')
depends=(
    'curl'
    'expat'
    'gcc-libs'
    'glibc'
    'libarchive'
    'libuv'
    'ncurses'
    'nghttp2'
    'zlib'
)
source=(https://cmake.org/files/v${pkgver%.*}/${pkgname}-${pkgver}.tar.gz)
sha256sums=(81ee8170028865581a8e10eaf055afb620fa4baa0beb6387241241a975033508)

build() {
    cd ${pkgname}-${pkgver}

    CC=${CHOST}-gcc          \
    CXX=${CHOST}-g++         \
    ./bootstrap              \
        --prefix=/usr        \
        --system-libs        \
        --mandir=/share/man  \
        --no-system-jsoncpp  \
        --no-system-cppdap   \
        --no-system-librhash \
        --docdir=/share/doc/${pkgname}-${pkgver} \
        --parallel=$(/usr/bin/getconf _NPROCESSORS_ONLN)

    make
}

package() {
    cd ${pkgname}-${pkgver}

    make DESTDIR=${pkgdir} install
}
