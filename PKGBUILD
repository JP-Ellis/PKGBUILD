# Maintainer: JP-Ellis <josh@jpellis.me>

pkgname=madgraph-pythia8-interface
pkgver=1.0
pkgrel=9
pkgdesc="MadGraph Pythia8 interface"
url="http://madgraph.hep.uiuc.edu/"
arch=('i686' 'x86_64')
license=('MIT')
depends=(
    'hepmc'
    'madgraph'
    'pythia'
    'python2'
)
source=(
    "http://madgraph.phys.ucl.ac.be/Downloads/MG5aMC_PY8_interface/MG5aMC_PY8_interface_V${pkgver}.tar.gz"
    "python2.patch"
    "pythia.patch"
)
sha256sums=('dd1a96f598176c3eb5f91bc189eaac1405afebf23f7fcfd055135d788dc69e3d'
            '632adc73e951df4341709adeafd3a7c72da1752f8af61037eae2b87a08ca9a64'
            'e506dad2224ed639a83537b21eadeda0ee244e9b5d5ee2770e536564f1e41491')

prepare() {
    msg2 "Fixing python references for python2"
    patch -p 1 < python2.patch

    msg2 "Fixing Pythia location"
    patch -p 1 < pythia.patch
}

build() {
    ./compile.py --pythia8_makefile /usr /opt/madgraph
}

package() {
    msg2 "Installing files"

    destdir="${pkgdir}/opt/madgraph/pythia8-interface"
    mkdir -p "${destdir}"
    install -Dm755 "${srcdir}/MG5aMC_PY8_interface" "${destdir}/MG5aMC_PY8_interface"
    install -Dm644 "${srcdir}/MG5AMC_VERSION_ON_INSTALL" "${destdir}/MG5AMC_VERSION_ON_INSTALL"
    install -Dm644 "${srcdir}/PYTHIA8_VERSION_ON_INSTALL" "${destdir}/PYTHIA8_VERSION_ON_INSTALL"
    install -Dm644 "${srcdir}/VERSION" "${destdir}/VERSION"
    install -Dm644 "${srcdir}/MultiHist.h" "${destdir}/MultiHist.h"
    install -Dm644 "${srcdir}/SyscalcVeto.h" "${destdir}/SyscalcVeto.h"
}

# Local Variables:
# mode: sh
# End:
