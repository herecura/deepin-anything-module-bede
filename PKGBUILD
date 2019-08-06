_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede
pkgver=5.0.1
pkgdesc="Kernel module for deepin-anything (linux-bede)"
_extramodules=5.2-BEDE-external
_current_linux_version=5.2.6
_next_linux_version=5.3
pkgrel=25
arch=('x86_64')
url="https://github.com/linuxdeepin/deepin-anything"
license=('GPL3')
makedepends=(
    "linux-bede>=$_current_linux_version"
    "linux-bede-headers>=$_current_linux_version"
    "linux-bede<$_next_linux_version"
    "linux-bede-headers<$_next_linux_version"
)
depends=(
    "linux-bede>=$_current_linux_version"
    "linux-bede<$_next_linux_version"
)
provides=('DEEPIN-ANYTHING-MODULE')
source=("$_pkgname-$pkgver.tar.gz::https://github.com/linuxdeepin/deepin-anything/archive/$pkgver.tar.gz")
sha512sums=('f79b4db917cce2611bd6964d00ae0e162fc500fa7ca76a987145456a9ee81296c776d2b83cf6492a4224c4e4fd95df3ad95a25c1c14d2d4e6865f5bbd639be14')

#prepare() {
    #cd $_pkgname-$pkgver
#}

build() {
    _kernver="$(cat /usr/lib/modules/${_extramodules}/version)"

    cd $_pkgname-$pkgver
    make -C kernelmod kdir=/usr/lib/modules/$_kernver/build
}

package() {
    cd $_pkgname-$pkgver/kernelmod
    install -dm 755 "$pkgdir"/usr/lib/modules/$_extramodules/deepin
    install -m 644 vfs_monitor.ko "$pkgdir"/usr/lib/modules/$_extramodules/deepin/
    find "${pkgdir}" -name '*.ko' -exec xz {} +
}

