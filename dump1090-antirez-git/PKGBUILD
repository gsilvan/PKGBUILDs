# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>

pkgname=dump1090-antirez-git
pkgver=r118.efe64db
pkgrel=1
pkgdesc="Mode S decoder written in C by antirez"
arch=(
    'x86_64'
    'armv7h'
    'aarch64'
)
url="https://github.com/antirez/dump1090"
license=('BSD-3-Clause')
depends=(
    'glibc'
    'rtl-sdr'
)
makedepends=('git')
provides=('dump1090')
conflicts=(
    'dump1090-fa-git'
    'dump1090-git'
    'dump1090-tomswartz-git'
    'dump1090-mutability-git'
    'dump1090-mictronics-git'
)
source=("$pkgname::git+$url.git")
sha256sums=('SKIP')

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
    install -Dm755 "dump1090" "$pkgdir/usr/bin/dump1090"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}

