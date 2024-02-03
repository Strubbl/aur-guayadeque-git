# $Id$
# Maintainer: Sven Fischer <aur.archlinux@linux4tw.de>

pkgname=guayadeque-git
_pkgname=guayadeque
pkgver=0.4.7.r2237.5e1ed7b2
pkgrel=1
pkgdesc='Lightweight music player'
arch=('i686' 'x86_64')
url='http://guayadeque.org/'
license=('GPL3')
provides=(${pkgname%-*})
conflicts=(${pkgname%-*})
depends=('curl' 'gst-plugins-base' 'jsoncpp' 'libgpod' 'taglib' 'webkit2gtk' 'wxgtk3' 'wxsqlite3')
makedepends=('cmake' 'git')
optdepends=('gst-plugins-good: Support for PulseAudio and additional file formats'
            'gst-plugins-bad: Support for additional file formats'
            'gst-plugins-ugly: Support for additional file formats'
            'gst-libav: Support for additional file formats'
            'gvfs: Support for external devices')
source=('git+https://github.com/openmonk/guayadeque.git')
sha512sums=('SKIP')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  local srcversion="$(grep "ID_GUAYADEQUE_VERSION" src/Version.h.in | cut -d '"' -f 2)"
  printf "%s.r%s.%s" $srcversion "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${_pkgname}"
  ./buildt
  cmake . \
    -DCMAKE_CXX_STANDARD='11' \
    -DCMAKE_BUILD_TYPE='Release' \
    -DCMAKE_INSTALL_PREFIX='/usr' \
    -DwxWidgets_wxrc_EXECUTABLE='/usr/bin/wxrc-3.2' \
    -DwxWidgets_CONFIG_EXECUTABLE='/usr/bin/wx-config' \
    -DwxWidgets_INCLUDE_DIRS='/usr/include/wx-3.2/'
  make
}

package() {
  cd "${srcdir}/${_pkgname}"
  make DESTDIR="${pkgdir}" install
}
