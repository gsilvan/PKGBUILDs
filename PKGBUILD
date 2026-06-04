# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>

pkgname=meshtastic-sniffer-git
pkgver=r224.733a528
pkgrel=1
pkgdesc="Wideband Meshtastic LoRa receiver with multi-station fusion and offline PSK recovery"
arch=(
    'x86_64'
    'armv7h'
    'aarch64'
)
url="https://github.com/alphafox02/meshtastic-sniffer"
license=('GPL-3.0-or-later')
depends=(
    'glibc'
    'fftw'
    'openssl'
    'zlib'
    'libgomp'
)
makedepends=(
    'cmake'
    'go'
    'git'
)
optdepends=(
    'airspy'
    'bladerf'
    'hackrf'
    'libuhd'
    'libsdrplay'
    'libsodium'
    'mosquitto'
    'rtl-sdr'
    'soapysdr'
    'zeromq'
)
provides=(
    'meshtastic-sniffer'
    'meshtastic-recover'
    'meshtastic-fusion'
    'meshtastic-wardrive'
)
conflicts=(
    'meshtastic-sniffer'
)
source=("$pkgname::git+$url.git")
sha256sums=('SKIP')

pkgver() {
    cd "$pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

build() {
    cd "$pkgname"
    export GOPATH="${srcdir}"
    export CGO_CPPFLAGS="${CPPFLAGS}"
    export CGO_CFLAGS="${CFLAGS}"
    export CGO_CXXFLAGS="${CXXFLAGS}"
    export CGO_LDFLAGS="${LDFLAGS}"
    export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
    cmake .
    make
    cd "fusion"
    go build
    cd "../wardrive"
    go build
}

package() {
    cd "$pkgname"
    install -Dm755 "meshtastic-sniffer" "$pkgdir/usr/bin/meshtastic-sniffer"
    install -Dm755 "meshtastic-recover" "$pkgdir/usr/bin/meshtastic-recover"
    install -Dm755 "fusion/meshtastic-fusion" "$pkgdir/usr/bin/meshtastic-fusion"
    install -Dm755 "wardrive/meshtastic-wardrive" "$pkgdir/usr/bin/meshtastic-wardrive"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}

