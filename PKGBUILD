# Contributor: Cian Mc Govern <cian [at] cianmcgovern [dot] com>
# Contributor: Roland Singer <roland [at] manjaro [dot] org>
# Contributor: TheBenj <thebenj88 [at] gmail [dot] com>
# Contributor: Philipp 'TamCore' B. <philipp [at] tamcore [dot] eu>
# Maintainer: William Overstreet <william.ab.overstreet@gmail.com>

pkgname=crossover
pkgver=15.0.0
pkgrel=1
_pkgdebrel=1
pkgdesc="Run Windows Programs on Linux"
arch=('i686' 'x86_64')
url="http://www.codeweavers.com"
license=('custom:CrossOver Linux License Grant')
changelog="CHANGELOG"
makedepends=('tar')
install=${pkgname}.install
replaces=('crossover-games' 'crossover-pro' 'crossover-standard')

source=("http://media.codeweavers.com/pub/${pkgname}/cxlinux/demo/${pkgname}_${pkgver}-${_pkgdebrel}.deb")
sha256sums=('b1ce956746d5dae8f21ead6b243e914d480d65513d4669db0e35e84aa764c5a0')

depends=( 
    'python2' 'desktop-file-utils' 'pygtk' 'python2-dbus'
)

optdepends=(
    'unzip: required to install Guild Wars, automatic installer extraction'
)

depends_i686=(
    'glibc>=2.11' 'libice' 'libsm' 'libx11' 'libxext' 'libxi' 'freetype2'
    'libpng' 'zlib' 'lcms2' 'libgl' 'libxcursor' 'libxrandr' 'glu'
)

optdepends_i686=(
    'alsa-lib: This is the preferred way to provide audio support to Windows applications.'
    "fontconfig: Makes it possible to find and use the system's TrueType fonts. This is strongly recommended for office-type applications."
    'gnutls: This is needed by applications that perform encryption or check online certificates.'
    'gsm: Lets Windows applications use the GSM codec for audio compression and decompression.'
    'gstreamer0.10: This is needed by some games and multimedia applications.'
    'gstreamer0.10-base: This is needed by some games and multimedia applications.'
    'isdn4k-utils: (libcapi)Provides support for some ISDN cards. Very few applications need this.'
    'libcups: Needed to print to printers managed by the CUPS system, which is most likely the case. It is strongly recommended for office-type applications.'
    'libdbus: This is needed for Windows applications to automatically detect CD-ROM and USB key insertion.'
    'libexif: Some applications need to parse EXIF and read their data tags.'
    'libgphoto2: Lets Windows applications access digital cameras.'
    'libldap: Lets Windows applications access LDAP servers.'
    'libxcomposite: This is needed for most CAD-like applications and some games.'
    "libxinerama: This is needed if your display spans multiple screens. If your computer has a single screen then you don't need it."
    'libxml2: This library makes it possible for Windows applications read and write XML files.'
    'libxslt: This library lets Windows applications perform queries and transformations on XML files.'
    'libxxf86vm: This is needed to let games perform some gamma adjustments (essentially to adjust the brightness).'  
    'libxxf86dga: X11 Direct Graphics Access extension library.' 
    'mpg123: Needed by some Windows applications to play MP3 files.'
    'nss-mdns: Host name resolution via mDNS'
    'ocl-icd: OpenCL ICD Bindings'
    'openal: Provides audio support to Windows applications.' 
    'openssl: This library provides support for secure Internet communication.'
    'sane: Lets Windows applications access scanners.'
    'v4l-utils: Lets Windows applications access video devices.' 
)

depends_x86_64=(
    'lib32-glibc>=2.11' 'lib32-libice' 'lib32-libsm' 'lib32-libx11'
    'lib32-libxext' 'lib32-libxi' 'lib32-freetype2' 'lib32-libpng' 'lib32-zlib'
    'lib32-lcms2' 'lib32-libgl' 'lib32-libxcursor' 'lib32-libxrandr'
    'lib32-glu'
)

optdepends_x86_64=(
    'lib32-alsa-lib: This is the preferred way to provide audio support to Windows applications.'
    "lib32-fontconfig: Makes it possible to find and use the system's TrueType fonts. This is strongly recommended for office-type applications."
    'lib32-libcups: Needed to print to printers managed by the CUPS system, which is most likely the case. It is strongly recommended for office-type applications.'
    'lib32-libdbus: This is needed for Windows applications to automatically detect CD-ROM and USB key insertion.'
    'lib32-libexif: (aur) Some applications need to parse EXIF and read their data tags.'
    'lib32-libldap: Lets Windows applications access LDAP servers.'
    'lib32-gnutls: This is needed by applications that perform encryption or check online certificates.'
    'lib32-gsm: (aur) Lets Windows applications use the GSM codec for audio compression and decompression.'
    'lib32-gstreamer0.10: (aur) This is needed by some games and multimedia applications.'
    'lib32-gstreamer0.10-base: (aur) This is needed by some games and multimedia applications.'
    'lib32-libgphoto2: (aur) Lets Windows applications access digital cameras.'
    'lib32-libxcomposite: This is needed for most CAD-like applications and some games.'
    "lib32-libxinerama: This is needed if your display spans multiple screens. If your computer has a single screen then you don't need it."
    'lib32-libxml2: This library makes it possible for Windows applications read and write XML files.'
    'lib32-libxslt: This library lets Windows applications perform queries and transformations on XML files.' 
    'lib32-libxxf86vm: This is needed to let games perform some gamma adjustments (essentially to adjust the brightness).'  
    'lib32-libxxf86dga: X11 Direct Graphics Access extension library.' 
    'lib32-mpg123: Needed by some Windows applications to play MP3 files.'
    'lib32-nss-mdns: (aur) host name resolution via mDNS'
    'lib32-libcl: OpenCL bindings provided by nvidia'
    'lib32-openal: Provides audio support to Windows applications.' 
    'lib32-openssl: This library provides support for secure Internet communication.'
    'lib32-sane: (aur) Lets Windows applications access scanners.'
    'lib32-v4l-utils: Lets Windows applications access video devices.' 
)

package() {
    cd ${srcdir}

    ar -p crossover_${pkgver}-${_pkgdebrel}.deb data.tar.gz | tar zxf - -C "${pkgdir}" || return 1
    if [[ "${CARCH}" = 'i686' ]]; then
        rm -f ${pkgdir}/opt/cxoffice/lib/nsplugin-linux64.so
    fi

    #remove symlink and create real directory
    rm ${pkgdir}/opt/cxoffice/doc 
    mkdir ${pkgdir}/opt/cxoffice/doc 

    mv ${pkgdir}/usr/share/doc/crossover/* ${pkgdir}/opt/cxoffice/doc

    gzip -d "${pkgdir}/opt/cxoffice/doc/license.txt.gz"
    rm -r "${pkgdir}/usr"
    sed -e 's!;;"MenuRoot" = ""!"MenuRoot" = "Windows Games"!' \
        -e 's!;;"MenuStrip" = ""!"MenuStrip" = "1"!' \
        -i ${pkgdir}/opt/cxoffice/share/crossover/bottle_data/cxbottle.conf

    mkdir -p ${pkgdir}/usr/bin
    ln -s /opt/cxoffice/bin/crossover ${pkgdir}/usr/bin/crossover
    ln -s /opt/cxoffice/bin/cxsetup ${pkgdir}/usr/bin/cxsetup

    mkdir -p ${pkgdir}/etc/profile.d
    echo '[ -d /opt/cxoffice/bin ] && export PATH="${PATH}:/opt/cxoffice/bin"' > ${pkgdir}/etc/profile.d/cxoffice.sh
    echo '[ -d /opt/cxoffice/bin ] && setenv PATH ${PATH}:/opt/cxoffice/bin' > ${pkgdir}/etc/profile.d/cxoffice.csh
    chmod 755 ${pkgdir}/etc/profile.d/cxoffice.sh ${pkgdir}/etc/profile.d/cxoffice.csh

    # Fix Auto update error
    install -m 644 -D ${pkgdir}/opt/cxoffice/share/crossover/data/cxoffice.conf ${pkgdir}/opt/cxoffice/etc/cxoffice.conf
    sed -e 's!;;"PrivateShortcutDirs" = ""!"PrivateShortcutDirs" = "${HOME}/bin:${CX_ROOT}/bin"!' \
        -e 's!;;"PrivateLinuxNSPluginDirs" = ""!"PrivateLinuxNSPluginDirs" = "${MOZ_PLUGIN_PATH}"!' \
        -e 's!;;"PrivateLinux64NSPluginDirs" = ""!"PrivateLinux64NSPluginDirs" = "${MOZ_PLUGIN_PATH}"!' \
        -e 's!;;"ProductPackage" = ""!"ProductPackage" = "Converted from .deb to pacman."!' \
        -i ${pkgdir}/opt/cxoffice/etc/cxoffice.conf

    # Changelog for pacman -Qc
    gzip -dfc ${pkgdir}/opt/cxoffice/doc/changelog.Debian.gz > ${startdir}/CHANGELOG

    # place license in correct directory
    install -D -m644 ${pkgdir}/opt/cxoffice/doc/license.txt ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
}
