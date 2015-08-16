# Author: Daniel Kozak <kozzi11@gmail.com>
pkgname=hhvm-pgsql
pkgver=3.6.0
pkgrel=2
pkgdesc="PostgreSQL extension for HHVM"
arch=('i686' 'x86_64')
url="https://github.com/PocketRent/$pkgname"
license=(PHP)
depends=('hhvm=3.6.0' 'postgresql-libs')
makedepends=('git' 'cmake')
source=("$pkgname.tar.gz::https://github.com/PocketRent/$pkgname/archive/3.6.0.tar.gz")

prepare() {
    cd "${srcdir}/${pkgname}-$pkgver"
    mkdir -p build    
    cp ext_pgsql.php build/
    hphpize
    cd build
    cmake ".."
}

build() {
    cd "${srcdir}/${pkgname}-$pkgver/build"
    make
}

package() {
    cd "${srcdir}/${pkgname}-$pkgver/build"
    make DESTDIR="${pkgdir}" install
    mv "$pkgdir"/usr/lib{64,}
    mv "$pkgdir"/usr/lib/hhvm/extensions/20150212/pgsql.so "$pkgdir"/usr/lib/hhvm/extensions/pgsql.so
    rmdir "$pkgdir"/usr/lib/hhvm/extensions/20150212
    install -Dm644 "${srcdir}/${pkgname}-$pkgver/LICENSE.PHP" "$pkgdir/usr/share/licenses/$pkgname/LICENSE.PHP"
}

# vim:set ts=2 sw=2 et:
sha256sums=('6cdea4274dd02034fdf566356dc133a5ab7ecc86d7fc8d76fb294e4785b386e7')
