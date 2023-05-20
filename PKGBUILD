# Maintainer: JP-Ellis <josh@jpellis.me>
pkgname=python-doi
_name=${pkgname}
pkgver=0.2.0
pkgrel=1
pkgdesc="Python package to work with Document Object Identifier (doi)."
arch=('any')
url="https://pypi.org/project/python-doi"
license=('BSD')
depends=('python')
makedepends=('python-setuptools')
source=("https://files.pythonhosted.org/packages/source/${_name::1}/${_name}/${_name}-${pkgver}.tar.gz")
sha256sums=('2e01e56fb319bd219ea8586baa43a1fc794dfe45a83156ac70242c4ce961fd9a')

build() {
  cd "${srcdir}/${_name}-${pkgver}"
  python setup.py build
  touch Changelog.rst
}

package() {
  cd "${srcdir}/${_name}-${pkgver}"
  python setup.py install --root="$pkgdir/" --optimize=1 --skip-build
}

# vim:ts=2:sw=2:et:
