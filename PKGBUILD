# Maintainer: Jeancarlo Hidalgo <jeancahu [at] gmail [dot] com>

pkgname=firmadigital
pkgver=26
pkgrel=1
arch=('x86_64')
pkgdesc="AgenteGaudi para FirmaDigital Costa Rica, Linux client for Costa Rica FirmaDigital"
license=('custom')
depends=('pcsclite' 'ccid') # Dependencias mostradas en lib.sh
install=firmadigital.install
options=(!strip docs libtool emptydirs !zipman staticlibs)
source=(
    "sfd_ClientesLinux_DEB64_Rev26.zip"
    "firma-digital.module" # fran.cr
    "IDPClientDB.xml" # fran.cr
)
md5sums=(
    '56da38a0f5b8c18aa2001ee55f14c450'
    '6d1e071b3edbadf57858fb6d64cefe2a'
    'd8a9bc85f2e8410b92b352d5d28ac938'
)

prepare() {
    echo "========================================"
    echo "Remember: The source file sfd_ClientesLinux_DEB64_Rev26.zip must be downloaded manually."
    echo "Download it from: https://soportefirmadigital.com/sfdj/dl.aspx?lang=es"
    echo "========================================"

    # Ahora descomprimir el archivo ZIP, si ya está descargado manualmente
    if [ ! -f "$srcdir/sfd_ClientesLinux_DEB64_Rev26.zip" ]; then
        echo "ERROR: sfd_ClientesLinux_DEB64_Rev26.zip not found. Please download it manually."
        exit 1
    fi

    # Extraer el archivo ZIP
    unzip -o "$srcdir/sfd_ClientesLinux_DEB64_Rev26.zip" -d "$srcdir"
}

package() {
    # Rutas de los .deb dentro del ZIP
    local debs=(
        "$srcdir/sfd_ClientesLinux_DEB64_Rev26/Firma Digital/PinTool/IDProtect PINTool 7.24.02/DEB/idprotectclient_7.24.02-0_amd64.deb"
        "$srcdir/sfd_ClientesLinux_DEB64_Rev26/Firma Digital/PinTool/IDProtect PINTool 7.24.02/DEB/idprotectclientlib_7.24-0_amd64.deb"
        "$srcdir/sfd_ClientesLinux_DEB64_Rev26/Firma Digital/Agente GAUDI/agente-gaudi_20.0_amd64.deb"
    )

    # Extraer y copiar los archivos de cada .deb
    for deb in "${debs[@]}"; do

        debname=$(basename "${deb/.deb/}")
        mkdir $debname
        bsdtar -xf "$deb" -C "$srcdir/$debname"

        if [ -f "$srcdir/$debname/data.tar.xz" ]; then
            tar -xf "$srcdir/$debname/data.tar.xz" -C "$pkgdir"
        elif [ -f "$srcdir/$debname/data.tar.gz" ]; then
            tar -xvzf "$srcdir/$debname/data.tar.gz" -C "$pkgdir"
        else
            ## There is no data.tar.*
            exit 1
        fi
    done

    # Copiar certificados
    for cert in $srcdir/sfd_ClientesLinux*/Firma\ Digital/Certificados/*
    do
        certname=$( basename "${cert}" )
        install -Dm644 "${cert}" "${pkgdir}/usr/share/ca-certificates/trust-source/anchors/${certname}"
    done

    ### BEGIN Referencia https://fran.cr/instalar-firma-digital-costa-rica-manjaro-arch-linux/
    install -d "${pkgdir}/usr/lib/"
    install -d "${pkgdir}/usr/local/lib/"
    install -d "${pkgdir}/Firma_Digital/LIBRERIAS/"
    install -d "${pkgdir}/usr/lib/firefox/"

    mv $pkgdir/usr/lib/x64-athena/libASEP11.so $pkgdir/usr/lib/
    ln -s "/usr/lib/libASEP11.so" "${pkgdir}/usr/lib/x64-athena/"
    ln -s "/usr/lib/libASEP11.so" "${pkgdir}/usr/local/lib/"
    ln -s "/usr/lib/libASEP11.so" "${pkgdir}/Firma_Digital/LIBRERIAS/"
    ln -s "/usr/share/ca-certificates/trust-source/anchors" "${pkgdir}/Firma_Digital/CERTIFICADOS"
    ln -s "/usr/lib/p11-kit-proxy.so" "${pkgdir}/usr/lib/firefox/libosclientcerts.so"

    install -Dm644 "${srcdir}/IDPClientDB.xml" "${pkgdir}/etc/Athena/IDPClientDB.xml"
    install -Dm644 "${srcdir}/firma-digital.module" "${pkgdir}/usr/share/p11-kit/modules/firma-digital.module"
    ### END Referencia https://fran.cr/instalar-firma-digital-costa-rica-manjaro-arch-linux/

    # Crear el enlace simbólico a Agente-GAUDI
    if [ -f "$pkgdir/opt/Agente-GAUDI/bin/Agente-GAUDI" ]; then
        ln -sf /opt/Agente-GAUDI/bin/Agente-GAUDI "$pkgdir/usr/bin/agentegaudi"
    else
        echo "Error: No se encontró el ejecutable Agente-GAUDI."
        exit 1
    fi
}
