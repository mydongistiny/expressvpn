# Maintainer: Kyle Manna <kyle(at)kylemanna(dot)com>
# Co-Maintainer: WorMzy Tykashi <wormzy.tykashi@gmail.com>

pkgname=expressvpn
pkgver=3.70.0.2_1
pkgrel=1
pkgdesc="Proprietary VPN client for Linux"
arch=('x86_64' 'i686' 'armv7h')
depends=('glibc')
url="https://expressvpn.com"
license=('LicenseRef-custom')
options=(!strip)
install=expressvpn.install
_url="https://www.expressvpn.works/clients/linux"
source_x86_64=("${_url}/${pkgname}_${pkgver/_/-}_amd64.deb"{,.asc})
source_i686=("${_url}/${pkgname}_${pkgver/_/-}_i386.deb"{,.asc})
source_armv7h=("${_url}/${pkgname}_${pkgver/_/-}_armhf.deb"{,.asc})

sha512sums_x86_64=('be0349cca3432afe31a1a00bf459cca0e3d3c553925c8897f99e7e82ed14252f7db9e301f64b13c5e34dedaedf6da514c5debc0d908181fe494dc5396e15c546'
                   'SKIP')
sha512sums_i686=('91c75278958f26a0cfbf28e9f3ac43b85aff8972c263eabb9db41985fe11221562590eeb05463ea35494a133de20c34aeac1e69343c61ef015688987e5d1ec54'
                 'SKIP')
sha512sums_armv7h=('aceeaeebb0f2977a134eb6c16d18c8fa19a75a87c6a5f04205f845531b25f8222d9f5ed6bb54a54d255873a5e14d877b0c9810f62db7b450f61d7caafa2f10f2'
                   'SKIP')
validpgpkeys=('1D0B09AD6C93FEE93FDDBD9DAFF2A1415F6A3A38')

package() {
    # /usr/sbin is a symlink to /usr/bin, rewrite it. Upstream also install files to both /lib and /usr/lib
    # merge these and move to correct location
    bsdtar -C "${pkgdir}" -xf "${srcdir}/data.tar.gz" -s ":/usr/sbin:/usr/bin:" -s ":/usr/lib:/lib:"
    mv "${pkgdir}/lib" "${pkgdir}/usr/"

    install -dm755 "${pkgdir}/usr/share/licenses/${pkgname}"
    ln -s "/usr/share/doc/expressvpn/COPYRIGHT" "${pkgdir}/usr/share/licenses/${pkgname}/COPYRIGHT"

    install -dm755 "${pkgdir}/var/lib/expressvpn/certs"

    # Remove unused /etc
    rm -r "$pkgdir/etc/"
}
