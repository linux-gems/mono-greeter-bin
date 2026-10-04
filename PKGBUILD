# Maintainer: Ibrahim Rafi <rafiibrahim8 at hotmail dot com>

pkgname=mono-greeter-bin
_pkgname=mono-greeter
pkgver=0.1.2
pkgrel=1
pkgdesc="A keyboard-first greeter for greetd, in a terminal: cage + foot + ratatui (prebuilt binary)"
arch=('x86_64')
url="https://github.com/rafiibrahim8/mono-greeter"
license=('MIT')
depends=('cage' 'foot' 'gcc-libs' 'glibc' 'greetd' 'systemd')
optdepends=('ttf-hack-nerd: the intended font (otherwise the default monospace font)'
            'kwallet-pam: unlock KDE Wallet at login'
            'gnome-keyring: unlock GNOME Keyring at login'
            'xorg-xinit: X11 sessions (started through startx)')
provides=("${_pkgname}")
conflicts=("${_pkgname}")
backup=('etc/mono-greeter/foot.ini'
        'etc/pam.d/mono-greeter')
options=(!strip !debug)
install="${pkgname}.install"
source=("${_pkgname}-${pkgver}-linux-x86_64.tar.gz::${url}/releases/download/v${pkgver}/${_pkgname}-v${pkgver}-linux-x86_64.tar.gz")
sha256sums=('923c4cbcf08dbd54a3ef3f81746594eb3bb1bb22f9ecc3b1fdb9cf10471d9a78')

package() {
  cd "${_pkgname}-v${pkgver}-linux-x86_64"

  install -Dm755 mono-greeter "${pkgdir}/usr/bin/mono-greeter"
  install -Dm644 greetd.toml greetd-test-vt2.toml -t "${pkgdir}/usr/share/${_pkgname}/"

  # greetd runs mono-greeter through this drop-in (greetd --config), so greetd's own
  # /etc/greetd/config.toml is never edited.
  install -Dm644 greetd.service.d/mono-greeter.conf \
    "${pkgdir}/usr/lib/systemd/system/greetd.service.d/mono-greeter.conf"
  install -Dm644 pam.d/mono-greeter "${pkgdir}/etc/pam.d/mono-greeter"
  install -Dm644 foot.ini "${pkgdir}/etc/mono-greeter/foot.ini"
  install -Dm644 tmpfiles.conf "${pkgdir}/usr/lib/tmpfiles.d/${_pkgname}.conf"

  install -Dm644 README.md "${pkgdir}/usr/share/doc/${_pkgname}/README.md"
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
