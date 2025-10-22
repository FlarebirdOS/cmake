pkgname=cmake
pkgver=4.1.2
pkgrel=2
pkgdesc="A cross-platform open-source make system"
arch=('x86_64')
url="https://www.cmake.org/"
license=('BSD-3-Clause'
    'MIT-open-group'
    'Zlib'
    'Apache-2.0'
)
depends=(
    'cppdap'
    'curl'
    'expat'
    'gcc-libs'
    'glibc'
    'hicolor-icon-theme'
    'jsoncpp'
    'libarchive'
    'libuv'
    'ncurses'
    'rhash'
    'zlib'
)
makedepends=(
    'emacs'
    'git'
    'nlohmann-json'
    'python-sphinx'
    'qt6-qtbase'
)
source=(git+https://gitlab.kitware.com/cmake/cmake.git#tag=v${pkgver})
sha256sums=(63cd90c2d8fde3eb30532aa7af09a74b34c800faa5f6dd78efd023fb49501a06)

prepare() {
    cd ${pkgname}

    # Fix FindHDF5 for HDF5 built with cmake
    git cherry-pick -n a869b79c5921412c91fb71a761748ae5f7d3fb23
}

build() {
    cd ${pkgname}

    local configure_args=(
        --prefix=/usr
        --mandir=/share/man
        --docdir=/share/doc/cmake
        --datadir=/share/cmake
        --sphinx-man
        --sphinx-html
        --system-libs
        --qt-gui
        --parallel=$(/usr/bin/getconf _NPROCESSORS_ONLN)
    )

    export CC="${CHOST}-gcc"
    export CXX="${CHOST}-g++"

    ./bootstrap "${configure_args[@]}"

    make
}

package() {
    cd ${pkgname}

    make DESTDIR=${pkgdir} install

    rm -r ${pkgdir}/usr/share/doc/cmake/html/_sources
    emacs -batch -f batch-byte-compile ${pkgdir}/usr/share/emacs/site-lisp/cmake-mode.el
}
