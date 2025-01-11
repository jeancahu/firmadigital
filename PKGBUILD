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
)
md5sums=(
    '56da38a0f5b8c18aa2001ee55f14c450'
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

    # Crear el enlace simbólico a Agente-GAUDI
    if [ -f "$pkgdir/opt/Agente-GAUDI/bin/Agente-GAUDI" ]; then
        ln -sf /opt/Agente-GAUDI/bin/Agente-GAUDI "$pkgdir/usr/bin/agentegaudi"
    else
        echo "Error: No se encontró el ejecutable Agente-GAUDI."
        exit 1
    fi
}
