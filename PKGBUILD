# Maintainer: JP-Ellis <josh@jpellis.me>
pkgname=github-copilot-cli
_pkgname="@githubnext/$pkgname"
pkgver=0.1.29
pkgrel=1
pkgdesc="A CLI experience for letting GitHub Copilot help you on the command line"
arch=('any')
url="https://githubnext.com/projects/copilot-cli/"
license=('none')
makedepends=('npm' 'jq')
source=("https://registry.npmjs.org/${_pkgname}/-/$pkgname-$pkgver.tgz")
sha256sums=('db29c3ac63393604d254bb1060e28700a0815a1d052879a944c60263fc9b49d8')
noextract=("${pkgname}-${pkgver}.tgz")

package() {
  npm install -g --cache "${srcdir}/npm-cache" --prefix "${pkgdir}/usr" "${srcdir}/${pkgname}-${pkgver}.tgz"

  msg2 "Fixing file ownership"
  chown -R root:root "${pkgdir}"

  msg2 "Removing references to srcdir"
  find "$pkgdir" -name package.json -print0 | xargs -r -0 sed -i '/_where/d'

  local tmppackage="$(mktemp)"
  local pkgjson="$pkgdir/usr/lib/node_modules/${_pkgname}/package.json"
  jq '.|=with_entries(select(.key|test("_.+")|not))' "$pkgjson" > "$tmppackage"
  mv "$tmppackage" "$pkgjson"
  chmod 644 "$pkgjson"
}
