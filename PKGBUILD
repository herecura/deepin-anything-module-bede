_pkgname="deepin-anything"
pkgname=deepin-anything-module-bede
pkgver=0.0.9
pkgdesc="Kernel module for deepin-anything (linux-bede)"
_extramodules=5.1-BEDE-external
_current_linux_version=5.1.4
_next_linux_version=5.2
pkgrel=2
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
sha512sums=('31f7507221c995bcf2667ff59765c14eea0e0d2739debbe85be785f1290f3e84614e9e691c84434798f5dc427deaafe116171ea72e7b14b862c90e8107545bee')

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

