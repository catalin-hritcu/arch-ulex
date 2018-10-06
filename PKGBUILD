# Maintainer: Jacob Thomas Errington <aur@mail.jerrington.me>
# Contributor: Catalin Hritcu <catalin.hritcu@gmail.com>

pkgname="ulex"
pkgver="1.2"
pkgrel=1
pkgdesc="An OCaml lexer generator for Unicode"
arch=(x86_64)
url="https://github.com/whitequark/ulex"
license=('MIT')
depends=('ocaml' 'camlp4')
makedepends=('ocaml-findlib' 'ocamlbuild')
provides=($pkgname)
conflicts=($pkgname)
source=("https://github.com/whitequark/${pkgname}/archive/v${pkgver}.tar.gz")
sha512sums=('bfa0c03aa5546330c970b7250cadcc87e944c793189e9785389058b19624af71a3e5540a3a4775946b2e8a59bb7fa28d2635e5fd05a47dbcbbf34dacb68e15de')

prepare() {
    cd "$pkgname-$pkgver"
    # build native code as well
    sed -i '1s/.*/ALL=pa_ulex.cmxa ulexing.cmxa pa_ulex.cma ulexing.cma/' Makefile
}

build() {
    cd "$pkgname-$pkgver"
    make
    make doc
}

check() {
    cd "$pkgname-$pkgver"
}

package() {
    _DOCDIR="${pkgdir}/usr/share/doc/${pkgname}"

    cd "$pkgname-$pkgver"

    export OCAMLFIND_DESTDIR="${pkgdir}$(ocamlfind printconf destdir)"
    mkdir -p "${OCAMLFIND_DESTDIR}"
    make install

    # Install doc
    mkdir -p $_DOCDIR
    cp *.html *.css $_DOCDIR/
}
