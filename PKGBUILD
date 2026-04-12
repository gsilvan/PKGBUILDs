# Maintainer: Silvan Gümüsdere <silvan@trollbox.org>
# Contributor: Felix Golatofski <contact@xdfr.de>
# Contributor: Johannes Dewender  arch at JonnyJD dot net
# Contributor: Vlad M. <vlad@archlinux.net>
# Contributor: Timofey Titovets <nefelim4ag@gmail.com>

pkgname=elasticdump
pkgver=6.124.2
pkgrel=1
pkgdesc="Import and export tools for Elasticsearch"
arch=(any)
url="https://github.com/elasticsearch-dump/elasticsearch-dump"
license=('Apache-2.0')
depends=('nodejs>=8.0')
makedepends=(
    'jq'
    'npm'
)
source=("https://registry.npmjs.org/${pkgname}/-/${pkgname}-${pkgver}.tgz")
sha256sums=('982c272a08cd0611f114d3a0740749a4a0f94f6510f45744b7c0f5df1d9b0a8d')
noextract=("$pkgname-$pkgver.tgz")

package() {
    npm install -g --cache "${srcdir}/npm-cache" --prefix "${pkgdir}/usr" "${srcdir}/${pkgname}-${pkgver}.tgz"

    # Fix permissions
    chmod -R u=rwX,go=rX "$pkgdir"

    # npm gives ownership of ALL FILES to build user
    # https://bugs.archlinux.org/task/63396
    chown -R root:root "${pkgdir}"

    # Remove references to pkgdir
    find "$pkgdir" -type f -name package.json -print0 | xargs -0 sed -i "/_where/d"

    # Remove references to srcdir
    local tmppackage="$(mktemp)"
    local pkgjson="$pkgdir/usr/lib/node_modules/$pkgname/package.json"
    jq '.|=with_entries(select(.key|test("_.+")|not))' "$pkgjson" > "$tmppackage"
    mv "$tmppackage" "$pkgjson"
    chmod 644 "$pkgjson"
}

