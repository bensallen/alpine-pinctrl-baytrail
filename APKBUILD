# Contributor: Ben Allen <bensallen@me.com>
# Maintainer: Ben Allen <bensallen@me.com>
_flavor=${FLAVOR:-grsec}
_kpkg=linux-$_flavor
_realname=pps-gpio
_name=$_realname-$_flavor

pkgver=4.4.45
pkgrel=0

case $pkgver in
*.*.*)  _kernver=${pkgver%.*};;
*.*)    _kernver=${pkgver};;
esac

# source the kernel version
if [ -f ../linux-$_flavor/APKBUILD ]; then
    . ../linux-$_flavor/APKBUILD
    [ "$_kver" != "$pkgver" ] && die "$_name: Please update _kver to $pkgver"
    [ "$_kpkgrel" != "$pkgrel" ] && die "$_name: Please update _kpkgrel to $pkgrel"
fi

_kernelver=$pkgver-r$pkgrel
_abi_release=${pkgver}-${pkgrel}-${_flavor}

pkgname=$_name
pkgdesc="Out-of-tree build of pps-gpio until Alpine enables CONFIG_PPS_CLIENT_GPIO"
url="https://www.kernel.org/doc/Documentation/pps/pps.txt"
arch="all"
license="GPL2"
arch="all"
depends="linux-${_flavor}=${_kernelver}"
makedepends="linux-${_flavor}-dev=${_kernelver} linux-headers"
install=
install_if="linux-$_flavor=$_kernelver $_realname"
subpackages=
source="https://kernel.org/pub/linux/kernel/v4.x/linux-$_kernver.tar.xz"
_builddir="$srcdir"/linux-$_kernver/drivers/pps/clients

build() {
    make -C /lib/modules/$_abi_release/build M=$_builddir CONFIG_PPS_CLIENT_GPIO=m CONFIG_PPS_CLIENT_LDISC="" modules || return 1
}

package() {
    make -C /lib/modules/$_abi_release/build M=$_builddir CONFIG_PPS_CLIENT_GPIO=m INSTALL_MOD_PATH=$pkgdir modules_install || return 1
}
md5sums="9a78fa2eb6c68ca5a40ed5af08142599  linux-4.4.tar.xz"
sha256sums="401d7c8fef594999a460d10c72c5a94e9c2e1022f16795ec51746b0d165418b2  linux-4.4.tar.xz"
sha512sums="13c8459933a8b80608e226a1398e3d1848352ace84bcfb7e6a4a33cb230bbe1ab719d4b58e067283df91ce5311be6d2d595fc8c19e2ae6ecc652499415614b3e  linux-4.4.tar.xz"
