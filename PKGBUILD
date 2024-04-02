# Maintainer: Kyle Manna <kyle(at)kylemanna(dot)com>
# Co-Maintainer: WorMzy Tykashi <wormzy.tykashi@gmail.com>

pkgname=expressvpn
pkgver=3.67.0.0_1
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

sha512sums_x86_64=('1b595ba25ec592dce95d66a6718e6e0e8ff42abb91a0b9da1bcccc9667d26bf58390fb93315d46bfd5b4607e23cc47c7bb6f072c9ee2c5185fb62a9ae2c2f314'
                   'SKIP')
sha512sums_i686=('54326fe4786235a4bc526ab6f17107b72d96d2e60d5622277c84a8db81ae5095990e4917616487db7f97144532c1f66840a4a45502c7e5e35a615e88d1f624ac'
                 'SKIP')
sha512sums_armv7h=('4748bc8e571bebda0074fb3f9a199769e952390c367535d4b3903d12e4c301a438d022ac74b0f16fcebb058b53bbc5a2322da6f9866587561842937171258e78'
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
