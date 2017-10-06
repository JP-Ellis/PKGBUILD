# Maintainer: Konstantin Gizdov < arch at kge dot pw >
# Contributor: Joshua Ellis < josh at jpellis dot me >
# Contributor: Stefano Campanella < stefanocampanella1729 at gmail dot com >

pkgname=pythia
pkgver=8.2.30
_pkgid="${pkgname}${pkgver//./}"
pkgrel=1
pkgdesc="High-energy physics events generator."
arch=('i686' 'x86_64')
url="http://home.thep.lu.se/Pythia/"
license=('GPL')
provides=('pythia' 'pythia8')
depends=('bash' 'boost' 'boost-libs')
optdepends=('fastjet: fast jet finding in pp and e+e- collisions'
            'hepmc: storing collisions from Monte Carlo'
            'lhapdf: evaluate PDFs from discretised data files'
            'root: integrate with CERN ROOT data analysis framework')
install=pythia.install
source=("http://home.thep.lu.se/~torbjorn/pythia8/${_pkgid}.tgz"
        "pythia.sh"
        "pythia.install"
        "respect_lib_suffix.patch")
sha256sums=('332fad0ed4f12e6e0cb5755df0ae175329bc16bfaa2ae472d00994ecc99cd78d'
            '12fabaa56db80537b94a89de18f688f1258f467ed01b1ee6595efe75cde801d2'
            'f1796729b0403026382bca43329692f5356c8ec46fc2c09f799a8b3d12d49a6f'
            'c9c31223c0c38f8d844ee1f8c984d4b723b7d960f2e13fe7847325785736127b')
options=('!emptydirs')
_srcpath="${srcdir}/${_pkgid}"

prepare() {
    cd "${srcdir}/${_pkgid}"
    msg2 'Applying patches...'
    patch -p1 -i "${srcdir}/respect_lib_suffix.patch"
}

build() {
    cd "${srcdir}/${_pkgid}"
    _inc=/usr/include/
    _lib=/usr/lib/

    ./configure --prefix="/usr" \
                --prefix-include=${_inc} \
                --prefix-lib=${_lib} \
                --cxx-common="${CXXFLAGS} -fPIC -pthread" \
                --enable-shared \
                --with-boost \
                --with-boost-include=${_inc} \
                --with-boost-lib=${_lib} \
                --with-evtgen \
                --with-evtgen-include=${_inc} \
                --with-evtgen-lib=${_lib} \
                --with-fastjet3 \
                --with-fastjet3-include=${_inc} \
                --with-fastjet3-lib=${_lib} \
                --with-gzip \
                --with-gzip-include=${_inc} \
                --with-gzip-lib=${_lib} \
                --with-hepmc2 \
                --with-hepmc2-include=${_inc} \
                --with-hepmc2-lib=${_lib} \
                --with-hepmc3 \
                --with-hepmc3-include=${_inc} \
                --with-hepmc3-lib=${_lib} \
                --with-lhapdf5 \
                --with-lhapdf5-include=${_inc} \
                --with-lhapdf5-lib=${_lib} \
                --with-lhapdf6 \
                --with-lhapdf6-include=${_inc} \
                --with-lhapdf6-lib=${_lib} \
                --with-powheg \
                --with-powheg-include=${_inc} \
                --with-powheg-lib=${_lib} \
                --with-promc \
                --with-promc-include=${_inc} \
                --with-promc-lib=${_lib} \
                --with-python \
                --with-python-include=/usr/include/python3.6m/ \
                --with-python-lib=/usr/lib/python3.6/ \
                --with-root \
                --with-root-include=/usr/include/root/ \
                --with-root-lib=/usr/lib/root/
    make ${MAKEFLAGS}
}

package() {
    mkdir -p "${pkgdir}/usr"
    install -Dm755 "${srcdir}/${_pkgid}/bin/pythia8-config" "${pkgdir}/usr/bin/pythia8-config"
    install -D "${srcdir}/pythia.sh" "${pkgdir}/etc/profile.d/pythia.sh"

    cp -r "${srcdir}/${_pkgid}/include" "${pkgdir}/usr/"
    cp -r "${srcdir}/${_pkgid}/share" "${pkgdir}/usr/"
    cp -r "${srcdir}/${_pkgid}/examples" "${pkgdir}/usr/share/Pythia8/"

    install -Dm755 "${srcdir}/${_pkgid}/lib/libpythia8.so" "${pkgdir}/usr/lib/libpythia8.so"
    install -Dm755 "${srcdir}/${_pkgid}/lib/_pythia8.so" "${pkgdir}/usr/lib/python3.6/site-packages/_pythia8.so"
    install -Dm755 "${srcdir}/${_pkgid}/lib/pythia8.py" "${pkgdir}/usr/lib/python3.6/site-packages/pythia8.py"
}
