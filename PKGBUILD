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
conflicts=("${pkgname%-git}")
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
	cd "$srcdir/${pkgname%-git}"
	( set -o pipefail
		git describe --long --first-parent --match 'v[0-9]*' --dirty 2>/dev/null | sed -re 's/v//;s/-/.r/;s/-/./;s/-/_/;' ||
		printf "r%s.%s" "$(git rev-list --first-parent --count HEAD)" "$(git rev-parse --short HEAD)"
	)
}

check() {
	cd "$srcdir/${pkgname%-git}"
}

package() {
	cd "$srcdir/${pkgname%-git}"
}
