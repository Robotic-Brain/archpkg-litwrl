# -*- mode: shell-script; -*-
# Maintainer: Robotic-Brain <github@roboticbrain.de>
pkgname=litwrl
pkgver=20160303
pkgrel=1
pkgdesc="Life in the Woods Renaissance is a modpack for Minecraft."
arch=('any')
url="http://lifeinthewoods.ca"
license=(
    'GPL3'
    'custom:Minecraft'
    'custom:Minecraft Forge Public License'
    'custom:JNBT'
    'unknown'
)
depends=('java-runtime>=7')
makedepends=('git')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}" 'litwr')
replaces=()
backup=()
options=()
install=
source=(
    'http://lifeinthewoods.getitfromhere.co.uk/downloads/LifeInTheWoodsRenaissanceLauncher.zip'
    'git+https://github.com/Robotic-Brain/archpkg-litwrl.git'
)
noextract=()
md5sums=(
    '1befca5a5f18ac4b4497d9b3148ee156'
    'SKIP'
)

pkgver() {
    cd "$srcdir/archpkg-${pkgname%-git}"
    ( set -o pipefail
        git describe --long --first-parent --match 'v[0-9]*' --dirty 2>/dev/null | sed -re 's/v//;s/-/.r/;s/-/./;s/-/_/;' ||
        printf "r%s.%s" "$(git rev-list --first-parent --count HEAD)" "$(git rev-parse --short HEAD)"
    )
}

prepare() {
    cd "$srcdir"
    patch -Np1 -i "$srcdir/archpkg-${pkgname%-git}/patch.txt"
}

build () {
    cd "$srcdir"
    ./linux/install.sh
    sed -e '/^Path=/d'                                              \
        -e 's_^Exec=.*_/usr/bin/'"${pkgname%-git}"'_'               \
        -e 's_^Icon=.*_/usr/share/'"${pkgname%-git}"'/appicon.png_' \
        'Life in the Woods Renaissance.desktop' > "${pkgname%-git}.desktop"
}

check() {
    cd "$srcdir/${pkgname%-git}"
    #desktop-file-validate
}

package() {
    cd "$srcdir"
    install -Dm644 "${srcdir}/litwrl.jar" "${pkgdir}/usr/share/${pkgname%-git}/litwrl.jar"
    install -Dm644 "${srcdir}/utils/appicon.png" "${pkgdir}/usr/share/${pkgname%-git}/appicon.png"
    install -Dm644 -t "${pkgdir}/usr/share/doc/${pkgname%-git}/" "${srcdir}/manual/*"
    install -Dm644 -t "${pkgdir}/usr/share/doc/${pkgname%-git}/" "${srcdir}/INSTALL.TXT"
    install -Dm644 -t "${pkgdir}/usr/share/licenses/${pkgname%-git}/" "${srcdir}/licenses/*"
    install -Dm644 "${srcdir}/${pkgname%-git}.desktop" "${pkgdir}/usr/share/applications/${pkgname%-git}.desktop"
}
