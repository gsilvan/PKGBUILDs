# Maintainer: Silvan Gümüşdere <silvan@trollbox.org>

pkgname=rtl_icecast-git
pkgver=r19.6cc4023
pkgrel=1
pkgdesc="RTL-SDR Icecast streaming client"
arch=(
    'x86_64'
    'armv7h'
    'aarch64'
)
url="https://github.com/j0uni/rtl_icecast"
license=('MIT')
depends=(
    'lame'
    'libshout'
    'liquid-dsp'
    'rtl-sdr'
)
makedepends=('git')
provides=('rtl_icecast')
source=(
    "$pkgname::git+$url.git"
    "rtl-icecast.service"
)
sha256sums=(
    'SKIP'
    '863bf13db405e4637ee377136a9ec1dd887849a06229543a347ddb0a30b6295c'
)

pkgver() {
    cd "$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
    cd "$pkgname"
    make
}

package() {
    cd "$pkgname"
    install -Dm755 build/rtl_icecast "$pkgdir/usr/bin/rtl_icecast"
    install -Dm644 config.ini.example "$pkgdir/etc/rtl_icecast/config.ini"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
    install -Dm644 ../rtl-icecast.service "$pkgdir/usr/lib/systemd/system/rtl-icecast.service"
}

