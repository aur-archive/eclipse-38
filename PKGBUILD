# Maintainer: alex-no1 <sanja dot msg at gmx dot de>
# Contributor: alex-no1 <sanja dot msg at gmx dot de>

pkgname=eclipse-38
_realname=eclipse
pkgver=3.8
_internal_pkgver=3.8.0
pkgrel=3
_date=201206081200
pkgdesc="An IDE for Java and other languages - 3.8 - simultaneously released with 4.2 Juno."
arch=('i686' 'x86_64')
url="http://www.eclipse.org/"
license=('EPL')
depends=('desktop-file-utils' 'gtk2'  'unzip'  'libwebkit'  'libxtst' 'python2')
provides=(${_realname})
conflicts=(${_realname} 'xulrunner')
install=${pkgname}.install
source=("http://download.eclipse.org/eclipse/downloads/drops/R-${pkgver}-${_date}/${_realname}-SDK-${pkgver}-linux-gtk.tar.gz"
        "eclipse.desktop"
        "eclipse.ini.patch"
        "eclipse.sh")
md5sums=('88e2ee3e6efd10bd83e13dc5422dff15'
         'cdfccaa0ebc257cd62e4da74e9c5e3b9'
         '808ab979cd5b150023d2ec3487cef6a3'
         '7ea99a30fbaf06ec29261541b8eb1e23')
[ "${CARCH}" = "x86_64" ] && source[0]="http://download.eclipse.org/eclipse/downloads/drops/R-${pkgver}-${_date}/${_realname}-SDK-${pkgver}-linux-gtk-${CARCH}.tar.gz"
[ "${CARCH}" = "x86_64" ] && md5sums[0]='c31df92e540ca65652aca0255f7f49a1'

package() {
  cd "${srcdir}/eclipse"

  # patch to increase default memory limits
  patch -Np0 -i ${srcdir}/eclipse.ini.patch

  # python2 fix
  sed -i 's|#!/usr/bin/python|#!/usr/bin/python2|' \
    plugins/org.apache.ant_1.8.3.v20120321-1730/bin/runant.py

  # install eclipse
  install -d -m755 ${pkgdir}/usr/share/${_realname}
  cp -r * ${pkgdir}/usr/share/${_realname}/

  # install bin file
  install -d -m755 ${pkgdir}/usr/bin
  install -m755 ${srcdir}/${_realname}.sh ${pkgdir}/usr/bin/${_realname}

  # install icon and desktop files
  install -d -m755 ${pkgdir}/usr/share/{applications,pixmaps}
  install -m644 ${srcdir}/${_realname}.desktop ${pkgdir}/usr/share/applications/
  install -m644 plugins/org.eclipse.sdk_${_internal_pkgver}.v${_date}/${_realname}48.png \
    ${pkgdir}/usr/share/pixmaps/${_realname}.png
}
