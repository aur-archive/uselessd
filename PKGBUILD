# Maintainer: Jack L. Frost <fbt@fleshless.org>
# vim: ft=sh syn=sh et

pkgdesc="A fork of systemd aiming to provide the init system parts of systemd only."
pkgname=( 'uselessd' 'libsystemd-uselessd' )
pkgver=8
pkgrel=2
arch=( 'i686' 'x86_64' )
url="http://uselessd.darknedgy.net"
license=( 'GPL2' 'LGPL2.1' 'MIT' )

makedepends=(
    'dbus' 'libcap' 'kmod' 'pam' 'acl' 'attr' 'python'
    'intltool' 'docbook-xsl' 'libxslt' 'gperf' 'linux-api-headers'
)

options=( 'strip' )
source=(
    "https://bitbucket.org/Tarnyko/uselessd/downloads/uselessd-${pkgver}.tar.xz"
    'uselessd.install'
)

build() {
  cd "${pkgname}-${pkgver}"

  ./configure \
    --libexecdir=/usr/lib \
    --localstatedir=/var \
    --sysconfdir=/etc \
    --with-sysvinit-path= \
    --with-sysvrcnd-path=

  make
}

package_uselessd() {
    pkgdesc="A fork of systemd aiming to provide the init system parts of systemd only."
    license=( 'GPL2' 'LGPL2.1' 'MIT' )
    
    depends=(
        'acl' 'dbus' 'kmod' 'libcap' 'pam' 'device-mapper'
        'libsystemd-uselessd' 'util-linux'
    )

    provides=( "uselessd=${pkgver}" )
    conflicts=( "systemd" )

    install='uselessd.install'

    make -C "$pkgname-$pkgver" DESTDIR="$pkgdir" install

    # Package the libs separately
    install -dm755 "${srcdir}/_libsystemd/usr/lib"
    mv "$pkgdir"/usr/lib/libsystemd* "${srcdir}/_libsystemd/usr/lib"
}

package_libsystemd-uselessd() {
    pkgdesc="systemd client libraries (the uselessd version)"
    license=( 'GPL2' )

    provides=( 'libsystemd-id128.so' 'libsystemd-daemon.so' )

    mv "$srcdir/_libsystemd"/* "$pkgdir"
}

md5sums=('8c8e69445a8e71f79d26a93aecbcddf2'
         'a0551c95d19ed6eaae35c8e2af58c987')
