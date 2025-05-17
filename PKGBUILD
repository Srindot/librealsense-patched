# Maintainer: pingplug < aur at pingplug dot me >
# Contributr: Patrick José Pereira < positivcheg94 at gmail dot com >

_RS4XX_VER=5.16.0.1
_SR300_VER=3.26.1.0
_L51X_VER=1.5.8.1
_L53X_VER=3.5.5.1

pkgname=librealsense
pkgver=2.55.1
pkgrel=2
pkgdesc="Intel® RealSense™ SDK 2.0 is a cross-platform library for Intel® RealSense™ depth cameras (D400 & L500 series and the SR300)."
arch=('x86_64')
url="https://github.com/IntelRealSense/librealsense"
license=('Apache')
makedepends=('cmake')
depends=('glfw' 'glu' 'gtk3' 'libusb')
source=(
  "https://github.com/IntelRealSense/librealsense/archive/refs/tags/v${pkgver}.tar.gz"
  "https://librealsense.intel.com/Releases/RS4xx/FW/D4XX_FW_Image-${_RS4XX_VER}.bin"
  "https://librealsense.intel.com/Releases/SR300/FW/SR3XX_FW_Image-${_SR300_VER}.bin"
  "https://librealsense.intel.com/Releases/L5xx/FW/L51X_FW_Image-${_L51X_VER}.bin"
  "https://librealsense.intel.com/Releases/L5xx/FW/L53X_FW_Image-${_L53X_VER}.bin"
  "realsense-viewer.desktop"
  "cstdint-fix.patch"
)
sha256sums=(
  '54546d834ff5d8b35d9955319ad2e428f6d9ae4c61b932d1bd716ed81ad135f7'
  'a481376ac2d072de1d057fe73d74fcc00ab5da17aa63fa92c18bb8f65adf909c'
  'c4ac2144df13c3a64fca9d16c175595c903e6e45f02f0f238630a223b07c14d1'
  '87a9a91b613d9d807b2bfc424abe9cac63cad75dfc04718592c44777cb0b4452'
  'b837b2cff2b270b89eed3c0b212ab4108389a20b6e07c19dd5957918ff9ce7e0'
  '59281f91e7d471a7dde1cf7207eddd8624e05218cc4301ee52e4c453a0c8ab21'
  'b33320244df2ccf00ca76fb992849c4aab5191d67ad4ab3866c465c175f8b12c'
)



prepare(){
  cd "${srcdir}/${pkgname}-${pkgver}"
  sed -i 's|, GROUP:="plugdev"||g' "config/99-realsense-libusb.rules"
  sed -i 's|, GROUP="plugdev"||g' "config/99-realsense-libusb.rules"

  mkdir -p build/common/fw/
  cp "../D4XX_FW_Image-${_RS4XX_VER}.bin" build/common/fw/
  cp "../SR3XX_FW_Image-${_SR300_VER}.bin" build/common/fw/
  cp "../L51X_FW_Image-${_L51X_VER}.bin" build/common/fw/
  cp "../L53X_FW_Image-${_L53X_VER}.bin" build/common/fw/
  cd "$srcdir/$pkgname-$pkgver"
  patch -p1 < ../cstdint-fix.patch
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  mkdir -p build && cd build
  CFLAGS="${CFLAGS} -Wformat -pthread" \
  CXXFLAGS="${CXXFLAGS} -Wformat -pthread" \
  unset HOME
  cmake .. \
    -DCMAKE_POLICY_VERSION_MINIMUM=3.5 \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_INSTALL_SBINDIR=bin \
    -DCMAKE_INSTALL_SYSCONFDIR=/etc \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_SHARED_LIBS=on \
    -DBUILD_WITH_STATIC_CRT=off \
    -DBUILD_WITH_OPENMP=on \
    -DBUILD_EXAMPLES=true \
    -DCHECK_FOR_UPDATES=off
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}/build"
  DESTDIR="${pkgdir}" make install
  # why install config file to ${HOME} ?
  install -dm755 "${pkgdir}/usr/share"
  mv "${pkgdir}/Documents/librealsense2" "${pkgdir}/usr/share"
  rmdir "${pkgdir}/Documents"
  cd "${srcdir}"
  install -Dm644 realsense-viewer.desktop "${pkgdir}/usr/share/applications/realsense-viewer.desktop"
  cd "${srcdir}/${pkgname}-${pkgver}"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 config/99-realsense-libusb.rules "${pkgdir}/etc/udev/rules.d/99-realsense-libusb.rules"
  install -Dm644 common/res/icon_512.png "${pkgdir}/usr/share/pixmaps/realsense-viewer.png"
}
