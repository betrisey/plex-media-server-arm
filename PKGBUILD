# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Rob Sletten <rsletten@gmail.com>
# Contributor: Tom Moore <t.moore01@gmail.com>
# Contributor: monty <linksoft@gmx.de>
# Contributor: Jon Wiersma <archaur@jonw.org>
# Contributor: Arthur <arthur.darcet@m4x.org>
# Contributor: Praekon <praekon@googlemail.com>
# Contributor: George Stelle <stelleg@gmail.com>

pkgname=plex-media-server
pkgver=0.9.11.7.803
_pkgsum=87d0708
pkgrel=1
pkgdesc='Plex Media Server'
arch=('i686' 'x86_64' 'arm')
url='https://plex.tv/'
license=('custom')
depends=('systemd')
replaces=('plexmediaserver')
conflicts=('plexmediaserver' 'plexmediaserver-plexpass')
backup=('etc/conf.d/plexmediaserver')
install='plex-media-server.install'
source=('plexmediaserver.conf.d'
        'plexmediaserver.service'
        'plexmediaserver.sh'
        'terms.txt')
source_i686=("https://downloads.plex.tv/plex-media-server/${pkgver}-${_pkgsum}/plexmediaserver-${pkgver}-${_pkgsum}.i386.rpm")
source_x86_64=("https://downloads.plex.tv/plex-media-server/${pkgver}-${_pkgsum}/plexmediaserver-${pkgver}-${_pkgsum}.x86_64.rpm")

source_arm=("https://downloads.plex.tv/plex-media-server/${pkgver}-${_pkgsum}/PlexMediaServer-${pkgver}-${_pkgsum}-arm.bin")

sha256sums=('a82829854ab8e780f7686a9e65d36c8cf6900d6c3471176e0f2aae8f5a024a19'
            'ea50f866c7aa6b0a9e71d830887fb081b70f34f0b4b36f7cd7a69ab48b81d371'
            '7e5e5e667739bd35f16b7de5edd5846b0ed555a0f61a17aa65e5d623e878f25d'
            '7bb97271eb2dc5d1dcb95f9763f505970d234df17f1b8d79b467b9020257915a')
sha256sums_i686=('23a8ef78472b80d5877b282cb8e2417db6fff5a8ee37c3e74fe7d2d0ea0c0396')
sha256sums_x86_64=('2586252f05df035a06f65b71ab1a01ced6fdc5c75b7d8d51ff8aafb795f04e46')
sha256sums_arm=('aaa5b140552ab92c39203a4ef646e3b6feea7e971579dae12e999c706d407abb')

package() {
  install -dm 755 "${pkgdir}"/{opt,etc/conf.d,usr/{bin,lib/systemd/system}}
 if [ "$CARCH" = "arm" ]; then
    tail -c `head -n 1 ../PlexMediaServer-${pkgver}-${_pkgsum}-arm.bin \
      | awk -Fsize= '{print $2}' \
      | cut -d, -f1` PlexMediaServer-${pkgver}-${_pkgsum}-arm.bin \
      | tar -xv 
    tar -xvf files.tgz
    tar -xvf tmp/rnxtmp/PlexMediaServer-${pkgver}-${_pkgsum}.tar.bz2
    rm -rf plexmediaserver
    mv PlexMediaServer-${pkgver}-${_pkgsum} plexmediaserver
    cp -dr --no-preserve='ownership' plexmediaserver "${pkgdir}"/opt/
  else 
    cp -dr --no-preserve='ownership' usr/lib/plexmediaserver "${pkgdir}"/opt/
  fi
  install -m 755 plexmediaserver.sh "${pkgdir}"/usr/bin/
  install -m 644 plexmediaserver.service "${pkgdir}"/usr/lib/systemd/system/
  install -m 644 plexmediaserver.conf.d "${pkgdir}"/etc/conf.d/plexmediaserver

  install -dm 755 "${pkgdir}"/var/lib/plex
  chown 421:421 -R "${pkgdir}"/var/lib/plex

  install -dm 755 "${pkgdir}"/usr/share/licenses/plex-media-server
  install -m 644 terms.txt "${pkgdir}"/usr/share/licenses/plex-media-server/
}

# vim: ts=2 sw=2 et:
