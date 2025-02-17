# Maintainer: Miquel Lionel <lionel at les-miquelots dot net>
# https://aur.archlinux.org/packages/honk-hg/

pkgname=honk-hg
_pkgname=honk
pkgver=1341.f74b9ce19463
pkgrel=2
epoch=0
pkgdesc="ActivityPub compatible server with web frontend. Mercurialtip."
arch=("x86_64")
url="https://humungus.tedunangst.com/r/honk"
license=("custom:ISC")
makedepends=("go" "sqlite")
depends=("go" "sqlite")
optdepends=("nginx: for TLS and reverse proxying")
changelog="$pkgname.changelog"
provides=("${pkgname}")
conflicts=("${pkgname}" 'honk')
source=("hg+https://humungus.tedunangst.com/r/honk")
sha512sums=('SKIP')
options=(strip zipman docs)
install="$_pkgname.install"

pkgver() {
    cd honk
    echo $(hg identify -n).$(hg identify -i)
}
    

build() {
    cd "$srcdir/honk"
    make all
}

package() {
   _PKG_HONKDIR="$pkgdir/usr/share/$_pkgname"
   _PKG_DOCDIR="$srcdir/$_pkgname/docs"
   _MANDIR="$pkgdir/usr/share/man/man"

   install -Dm755 "$srcdir/$_pkgname/$_pkgname" -t "$pkgdir/usr/bin"
   install -Dm644 "$srcdir/$_pkgname"/views/* -t "$_PKG_HONKDIR/views/"
   install -Dm644 "$_PKG_DOCDIR"/* -t "$_PKG_HONKDIR/docs/"
   
#  gzip -k -f $_PKG_DOCDIR/*.{1,3,5,7,8}
  for i in {1,3,5,8}; do
      install -Dm644 $_PKG_DOCDIR/honk.$i.gz -t ${_MANDIR}$i/
  done

   install -Dm644 $_PKG_DOCDIR/activitypub.7.gz ${_MANDIR}7/honk_activitypub.7.gz
   install -Dm644 $_PKG_DOCDIR/hfcs.1.gz ${_MANDIR}1/honk_hfcs.1.gz
   install -Dm644 $_PKG_DOCDIR/intro.1.gz ${_MANDIR}1/honk_intro.1.gz
   install -Dm644 $_PKG_DOCDIR/vim.3.gz ${_MANDIR}3/honk_vim.3.gz


   install -Dm644 "$srcdir/$_pkgname"/LICENSE -t "$pkgdir/usr/share/licenses/$_pkgname"
   install -Dm644 "../$_pkgname.service" -t "$pkgdir/usr/lib/systemd/system/"
}
