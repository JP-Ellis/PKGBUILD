# Maintainer: shulhan <ms@kilabit.info>

pkgname=google-cloud-ops-agent
pkgver=2.15.0
pkgrel=1
pkgdesc="Ops Agents that are part of the Google Cloud Operations product suite (specifically Cloud Logging and Cloud Monitoring)"
arch=(x86_64)
url='https://github.com/GoogleCloudPlatform/ops-agent'
license=('Apache License 2.0')
depends=('java-environment')
makedepends=(
	'cmake'
	'go'
	'git'
)
source=(
	"$pkgname::git+https://github.com/GoogleCloudPlatform/ops-agent.git"
	"fluent-bit::git+https://github.com/fluent/fluent-bit.git"
	"opentelemetry-operations-collector::git+https://github.com/GoogleCloudPlatform/opentelemetry-operations-collector.git"
	"opentelemetry-java-contrib::git+https://github.com/open-telemetry/opentelemetry-java-contrib.git"
)
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP')

prepare() {
	cd "${pkgname}"
	git submodule init
	git config submodule."submodules/fluent-bit".url \
	  "${srcdir}/fluent-bit"
	git config submodule."submodules/opentelemetry-operations-collector".url \
	  "${srcdir}/opentelemetry-operations-collector"
	git config submodule."submodules/opentelemetry-java-contrib".url \
	  "${srcdir}/opentelemetry-java-contrib"
	git submodule update

	# Replace Google Cloud Ops Agent prefix
	sed -i 's|prefix=/opt/google-cloud-ops-agent|prefix=/|' build.sh
}

build() {
	cd "${pkgname}"
	BUILD_DISTRO=arch \
	  CODE_VERSION="${pkgver}" \
	  DESDIR="${srcdir}/build" \
	  ./build.sh
}

package() {
	tar -xf /tmp/google-cloud-ops-agent.tgz -C ${pkgdir}/
}
