# Maintainer: Jeancarlo Hidalgo <jeancahu [at] gmail [dot] com>

pkgname=firmadigital
pkgver=27
pkgrel=1
arch=('x86_64')
pkgdesc="AgenteGaudi para FirmaDigital Costa Rica, Linux client for Costa Rica FirmaDigital"
license=('custom')
depends=('pcsclite' 'pcsc-tools' 'ccid') # Dependencias mostradas en lib.sh
install=firmadigital.install
options=(!strip docs libtool emptydirs !zipman staticlibs)
source=(
    "sfd_ClientesLinux_DEB64_Ubuntu24_Rev27.zip" # Nombre del paquete principal
)
md5sums=(
    'ded86e0bd6ce043a39526a66a4de5be8'
)

prepare() {
    echo "========================================"
    echo "Remember: The source file ${source[0]} must be downloaded manually."
    echo "Download it from: https://soportefirmadigital.com/sfdj/dl.aspx?lang=es"
    echo "========================================"

    # Ahora descomprimir el archivo ZIP, si ya está descargado manualmente
    if [ ! -f "$srcdir/${source[0]}" ]; then
        echo "ERROR: ${source[0]} not found. Please download it manually."
        exit 1
    fi

    # Extraer el archivo ZIP
    unzip -o "$srcdir/${source[0]}" -d "$srcdir"
}

package() {
    # Rutas de los .deb dentro del ZIP
    local debs=(
        "$srcdir/${source[0]/.zip/}/Firma Digital/Idopte/scmiddleware_idopte_6.23.32.0_ubun24_amd64.deb"
        "$srcdir/${source[0]/.zip/}/Firma Digital/Agente GAUDI/agente-gaudi_20.0_amd64.deb"
    )

    # Extraer y copiar los archivos de cada .deb
    install -d "${srcdir}/firmadigital"
    for deb in "${debs[@]}"; do

        debname=$(basename "${deb/.deb/}")
        install -d "${srcdir}/${debname}"
        bsdtar -xf "$deb" -C "$srcdir/$debname"

        if [ -f "$srcdir/$debname/data.tar.xz" ]; then
            tar -xf "$srcdir/$debname/data.tar.xz" -C "$srcdir/firmadigital"
        elif [ -f "$srcdir/$debname/data.tar.gz" ]; then
            tar -xvzf "$srcdir/$debname/data.tar.gz" -C "$srcdir/firmadigital"
        else
            ## There is no data.tar.*
            exit 1
        fi
    done

    ## Quitar permisos 777 a algunos ejecutables y archivos ya que es un hueco de seguridad
    find "${srcdir}/firmadigital/" -perm -0077 -exec chmod go-w {} +

    ## Mover los archivos de firmadigital al pkgdir
    cp -r "${srcdir}/firmadigital/"* "${pkgdir}"

    # Copiar certificados
    for cert in $srcdir/sfd_ClientesLinux*/Firma\ Digital/Certificados/*
    do
        certname=$( basename "${cert}" )
        install -Dm644 "${cert}" "${pkgdir}/usr/share/ca-certificates/trust-source/anchors/${certname}"
    done

    ### BEGIN Referencia https://fran.cr/instalar-firma-digital-costa-rica-manjaro-arch-linux/
    ## El artículo insta a utilizar el firmador libre:
    # "https://firmador.libre.cr/"
    # "https://firmador.libre.cr/firmador.jar"
    ### END Referencia https://fran.cr/instalar-firma-digital-costa-rica-manjaro-arch-linux/

    # Crear el enlace simbólico a Agente-GAUDI
    if [ -f "$pkgdir/opt/Agente-GAUDI/bin/Agente-GAUDI" ]; then
        ln -sf /opt/Agente-GAUDI/bin/Agente-GAUDI "$pkgdir/usr/bin/agentegaudi"
    else
        echo "Error: No se encontró el ejecutable Agente-GAUDI."
        exit 1
    fi
}
