# Maintainer: Kyle Manna <kyle(at)kylemanna(dot)com>
# Co-Maintainer: WorMzy Tykashi <wormzy.tykashi@gmail.com>

pkgname=expressvpn
pkgver=5.0.1.11498
pkgrel=1
pkgdesc="Proprietary VPN client for Linux"
arch=('x86_64')
depends=('libxkbcommon' 'libnl' 'iptables' 'psmisc' 'gcc-libs' 'brotli' 'iproute2' 'ca-certificates' 'mesa')
url="https://expressvpn.com"
license=('LicenseRef-custom')
options=(!strip)
install=expressvpn.install
source=("https://www.expressvpn.works/clients/linux/${pkgname}-linux-universal-${pkgver}.run")
sha512sums=(0ae5956bdd459478e3809c6cf11fcd2b2228f7a819d983a76a892d01a5b0236e7cdce2f61c558d06b559d2e310e837eba92909d88c1421a413eec9cd74590ca5)

build() {
    sh ${pkgname}-linux-universal-${pkgver}.run --target "${srcdir}/${pkgname}" --noexec --noexec-cleanup --nochown
}

package() {
    cd "${pkgname}/x64"

    # Install package files
    install -d "${pkgdir}/opt/${pkgname}"
    cp -r expressvpnfiles/bin/ "${pkgdir}/opt/${pkgname}"
    cp -r expressvpnfiles/lib/ "${pkgdir}/opt/${pkgname}"
    cp -r expressvpnfiles/plugins/ "${pkgdir}/opt/${pkgname}"
    cp -r expressvpnfiles/qml/ "${pkgdir}/opt/${pkgname}"
    cp -r expressvpnfiles/share/ "${pkgdir}/opt/${pkgname}"
    install -Dm 755 installfiles/error-notice.sh -t "${pkgdir}/opt/${pkgname}/bin"
    install -Dm 755 installfiles/run-in-terminal.sh -t "${pkgdir}/opt/${pkgname}/bin"

    # Link cli to /usr/bin
    install -d "${pkgdir}/usr/bin"
    ln -s /opt/${pkgname}/bin/expressvpnctl "${pkgdir}/usr/bin/expressvpnctl"

    # Create var path
    install -d "${pkgdir}/opt/${pkgname}/var"

    # Install systemd service
    install -Dm 644 "installfiles/${pkgname}-service.service" -t "${pkgdir}/etc/systemd/system"

    # Install desktop files
    install -Dm 644 "installfiles/app-icon.png" "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
    install -Dm 644 "installfiles/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

    # Install browser manifests
    sed -i "s|REPLACE_PATH|/opt/expressvpn/share/browser_helper_wrapper.sh|g" "${pkgdir}/opt/${pkgname}/share/chrome.com.expressvpn.helper.json"
    sed -i "s|REPLACE_PATH|/opt/expressvpn/share/browser_helper_wrapper.sh|g" "${pkgdir}/opt/${pkgname}/share/firefox.com.expressvpn.helper.json"
    install -Dm 644 "${pkgdir}/opt/${pkgname}/share/chrome.com.expressvpn.helper.json" "${pkgdir}/etc/chromium/native-messaging-hosts/com.expressvpn.helper.json"
    install -Dm 644 "${pkgdir}/opt/${pkgname}/share/chrome.com.expressvpn.helper.json" "${pkgdir}/etc/opt/chrome/native-messaging-hosts/com.expressvpn.helper.json"
    install -Dm 644 "${pkgdir}/opt/${pkgname}/share/firefox.com.expressvpn.helper.json" "${pkgdir}/etc/mozilla/native-messaging-hosts/com.expressvpn.helper.json"

    # Create user for service
    echo 'u expressvpn - "Proprietary VPN client for Linux"' |
      install -Dm644 /dev/stdin "${pkgdir}/usr/lib/sysusers.d/${pkgname}.conf"
    # Create group for Handshake DNS service
    echo 'u expressvpnhnsd - "Proprietary VPN client for Linux"' |
      install -Dm644 /dev/stdin "${pkgdir}/usr/lib/sysusers.d/${pkgname}hnsd.conf"
}
