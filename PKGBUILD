# Maintainer: JP-Ellis <josh@jpellis.me>

pkgname=checkmate
pkgver=2.0.3
pkgrel=4
pkgdesc="A program to compare theoretical models against many recent experimental analyses"
url="http://checkmate.hepforge.org/"
arch=('i686' 'x86_64')
license=('GPL3')
depends=("delphes"
         "fastjet"
         "hepmc"
         "madgraph"
         "pythia"
         "python2-scipy"
         "root")
source=("http://www.hepforge.org/archive/checkmate/CheckMATE-${pkgver}.tar.gz"
        "ExRootAnalysis.patch"
        "fastjet.patch"
        "path.patch"
        "PythiaHandler.patch")
sha256sums=('420fa42e4555e7f9f86605f7a17878fc9ff62cd852cbdd45f86361b3a27656a8'
            '9420c9b166261a67e2febe983c37638dcff85b3660b5fd4acf1733a52b0d9402'
            '55874c4a88f10b0307a1495028acfd7ad28f1fac6b170fcafbe3c01a5a0b0edb'
            '1092f5bf843ec51f8cf1510673218dadd220bca26209bbd03787fb4257e6a804'
            '89cff18a1bf2bea50238d455010157bbafaf2b6671fd2db97443bb6d283c6a94')

prepare() {
    msg2 "Patching files"
    patch -p 1 < ExRootAnalysis.patch
    patch -p 1 < fastjet.patch
    patch -p 1 < path.patch
    patch -p 1 < PythiaHandler.patch

    msg2 "Removing VCS directories"
    find . -type d -name ".svn" | xargs rm -rf
}

build() {
    msg2 "Compiling source"
    cd CheckMATE-${pkgver}
    ./configure --prefix="${pkgdir}/usr/" \
                --with-hepmc=/usr \
                --with-pythia=/usr \
                --with-gzipinc=/usr/include \
                --with-gziplib=/usr/lib \
                --with-python=/usr/bin/python2 \
                --with-rootsys=/usr \
                --with-delphes=/usr \
                --with-madgraph=/opt/madgraph
    make
    make AnalysisManager

    msg2 "Cleaning temporary build files"
    find . -type f -name "*.o" -o -name "*.lo" -print0 | xargs -0 rm -f

    msg2 "Compiling Python files"
    python2 -O -m compileall -qf . || true

}

package() {
    # CheckMATE does not provide `make install`; so we manually install files
    #
    # If any file is missing, I welcome a patch
    install -Dm755 "${srcdir}/CheckMATE-${pkgver}/bin/CheckMATE" "${pkgdir}/usr/bin/CheckMATE"
    install -Dm755 "${srcdir}/CheckMATE-${pkgver}/bin/AnalysisManager" "${pkgdir}/usr/bin/AnalysisManager"

    install -d "${pkgdir}/usr/share/CheckMATE"
    cp -r "${srcdir}/CheckMATE-${pkgver}/tools" "${pkgdir}/usr/share/CheckMATE"
    cp -r "${srcdir}/CheckMATE-${pkgver}/data" "${pkgdir}/usr/share/CheckMATE/"

    find "${pkgdir}" -type f -name "*.o" -delete

    find "${pkgdir}" -type d -name ".libs" -empty -delete
}

# Local Variables:
# mode: sh
# End:
