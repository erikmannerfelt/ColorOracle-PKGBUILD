pkgname=color-oracle
_pkgname="${pkgname}-java"
pkgver="13795737a360ea40b76d60020c48ce16df71b09c"
pkgrel=1
pkgdesc='Design for the color impaired, a color blindness simulator'
arch=('any')
url='http://colororacle.org/index.html'
license=('MIT')
depends=("java-runtime" "bash" "ant" "maven")
source=("https://github.com/erikmannerfelt/${_pkgname}/archive/${pkgver}.zip")
sha256sums=('f66c5d29c693163c6b72bf9a29269712a85ec5135d99a3b936a78c87e7667d32')

build() {
	cd "${srcdir}/${_pkgname}-${pkgver}"
	#sed -i 's/value="1.6"/value="1.7"/g' nbproject/build-impl.xml
	sed -i 's/javac\.source=1.6/javac\.source=1.8/g' nbproject/project.properties
	sed -i 's/javac\.target=1.6/javac\.target=1.8/g' nbproject/project.properties
	patch pom.xml "${srcdir}/../pom.xml.patch"

	mvn clean compile assembly:single
	mv target/*.jar "${srcdir}/ColorOracle.jar"
	cp LICENSE.txt "${srcdir}"

	echo -e "#!/usr/bin/bash\nXDG_CURRENT_DESKTOP=Unity java -jar /usr/share/java/${pkgname}/ColorOracle.jar" > "${srcdir}/${pkgname}"
}

package() {
  install -Dm644 "${srcdir}/ColorOracle.jar" \
    "${pkgdir}/usr/share/java/${pkgname}/ColorOracle.jar"

  install -Dm644 "${srcdir}/LICENSE.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"

  install -Dm755 "${srcdir}/${pkgname}" \
    "${pkgdir}/usr/bin/${pkgname}"

  install -Dm755 "${srcdir}/../ColorOracle.desktop" \
	  "${pkgdir}/usr/share/applications/ColorOracle.desktop"
}
