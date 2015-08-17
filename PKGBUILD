# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
# Contributor: Gabriel Martinez < reitaka at gmail dot com >
pkgname=qthaskell
pkgver=1.1.4.1
pkgrel=1
pkgdesc="A set of Haskell bindings for the Qt Widget Library from Nokia."
url="http://qthaskell.berlios.de/"
arch=('i686' 'x86_64')
license=('custom')
depends=('ghc' 'qt' 'haskell-opengl' 'haskell-cabal')
makedepends=('gcc' 'make' 'perl')
install=qthaskell.install
source=(http://download.berlios.de/qthaskell/qtHaskell-${pkgver}.tar.bz2)
md5sums=('cc5e284bcd88e8ea0e5b029850293159')

build() {
  cd ${srcdir}/qtHaskell-1.1.4

  find -name "*.pro" -exec sed -i "s|/usr/local|/usr|" {} \;

  ./build -qm || return 1
  cd qws
  make INSTALL_ROOT=${pkgdir} install || return 1

  cd ..
  runghc Setup configure --ghc --prefix=/usr --extra-lib-dirs=${pkgdir}/usr/lib || return 1
  ./build -b
  runghc Setup build || return 1

  runghc Setup register --gen-script || return 1
  runghc Setup unregister --gen-script || return 1
  runghc Setup copy --destdir=${pkgdir} || return 1

  install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh || return 1
  install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh || return 1

  install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE || return 1
}
