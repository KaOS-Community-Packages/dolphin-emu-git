pkgname=dolphin-emu-git
pkgver=4.0.2.r7725.3c475b9
pkgrel=1
pkgdesc='A GameCube / Wii / Triforce emulator'
arch=('x86_64')
url='http://www.dolphin-emu.org/'
license=('GPL2')
depends=('bluez' 'ffmpeg' 'libao' 'lzo2' 'miniupnpc' 'polarssl' 'portaudio-svn'
         'sdl2' 'sfml' 'soundtouch' 'wxgtk' 'xdg-utils' 'pulseaudio')
makedepends=('cmake' 'git')
provides=('dolphin-emu')
conflicts=('dolphin-emu')
options=('!emptydirs')
source=('dolphin-emu::git+https://github.com/dolphin-emu/dolphin.git')
sha256sums=('SKIP')

pkgver() {
  cd dolphin-emu

  _tag='4.0.2'

  printf "%s.r%s.%s" "${_tag}" "$(git rev-list --count ${_tag}..HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd dolphin-emu

  if [[ -d build ]]; then
    rm -rf build
  fi
  mkdir build && cd build

  cmake .. \
    -DCMAKE_INSTALL_PREFIX='/usr' \
    -DCMAKE_CXX_FLAGS='-fno-inline-functions' \
    -DENABLE_LTO='TRUE'
  make
}

package() {
  cd dolphin-emu/build

  make DESTDIR="${pkgdir}" install
  install -m 755 Binaries/dolphin-emu-nogui "${pkgdir}"/usr/bin/
}

# vim: ts=2 sw=2 et:
