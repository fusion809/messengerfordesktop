# Maintainer: Brenton Horne <brentonhorne77 at gmail dot com>
# Contributor: Michael Corrigan <ghost.vonage AT gmail DOT com>
# Contributor: tomsik68	<tomsik68 AT gmail DOT com>
# Contributor: gandl <gandlspam AT gmail DOT com>
# Contributor: Jristz <prflr88 AT gmail DOT com>
# Upstream URL: http://messengerfordesktop.com/

pkgname=messengerfordesktop
_pkgname=Facebook-Messenger-Desktop
pkgver=1.5.0.beta.1
_pkgver=1.5.0-beta.1
pkgrel=1
pkgdesc="Beautiful desktop client for Facebook Messenger. Chat without being distracted by your feed or notifications."
arch=('i686' 'x86_64')
url="http://messengerfordesktop.com/"
license=('MIT')
options=(!strip)
depends=('cairo' 'libxtst' 'alsa-lib' 'gtk2' 'gconf' 'libnotify' 'fontconfig' 'nss')
install=$pkgname.install
depends=('gcc-libs' 'cairo' 'libxtst' 'alsa-lib' 'gtk2' 'gconf' 'libnotify' 'fontconfig' 'nss' 'xorg-xprop' 'xorg-xwininfo')
makedepends=('git' 'gulp' 'npm')
source=("https://github.com/Aluxian/$_pkgname/archive/v$_pkgver.tar.gz"
				"start.sh")
md5sums=('c5840f31c39aa5108b9aaf438a916831'
         '5a931b534eb2367452eef527244af44f')
install="$pkgname.install"

if [ $(uname -m) == "i686" ]
 then
  _arch="linux32"
else
  _arch="linux64"
fi

build() {
  cd $_pkgname-$_pkgver
  npm install

  gulp build:${_arch}
}

package() {
	mkdir -p "${pkgdir}/usr/share/messengerfordesktop/"

	cd "${srcdir}/Facebook-Messenger-Desktop-${_pkgver}/build/Messenger/${_arch}"
	for file in `find . -type f`; do
	install -D -m644 "${file}" "${pkgdir}/usr/share/messengerfordesktop/${file}"
	done;

	cd "${srcdir}/Facebook-Messenger-Desktop-${_pkgver}/"
	install -D -m755 "${srcdir}/start.sh"	  							"${pkgdir}/usr/bin/messengerfordesktop"
	install -D -m755 "build/Messenger/${_arch}/Messenger"		"${pkgdir}/usr/share/messengerfordesktop/Messenger"
	install -D -m644 "assets-linux/messengerfordesktop.desktop" 	    "${pkgdir}/usr/share/applications/messengerfordesktop.desktop"
	install -D -m644 "assets-linux/icons/256/messengerfordesktop.png" "${pkgdir}/usr/share/pixmaps/messengerfordesktop.png"
	install -D -m644 "LICENSE" 										"${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

	sed -i '6s/.*/Exec=sh \/usr\/bin\/messengerfordesktop/' "${pkgdir}/usr/share/applications/messengerfordesktop.desktop"
}
