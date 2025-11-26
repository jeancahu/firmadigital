# Maintainer: Jeancarlo Hidalgo <jeancahu [at] gmail [dot] com>

pkgname=firmadigital
pkgver=29
pkgrel=1
arch=('x86_64')
pkgdesc="AgenteGaudi para FirmaDigital Costa Rica, Linux client for Costa Rica FirmaDigital"
license=('custom')

# Dependencias necesarias SOLAMENTE para construir el paquete (como 7z para extraer certificados de .EXE):
#makedepends=('p7zip')

depends=(
    #'jre17-openjdk' # Runtime de OPENJDK # TODO
    'libappindicator' # SCMiddleware dependency
    'pcsclite'
    'pcsc-tools'
    'ccid'
    # 'opensc' # TODO
) # Dependencias mostradas en lib.sh
install=firmadigital.install
options=(!strip docs libtool emptydirs !zipman staticlibs)
source=(
    "sfd_ClientesLinux_DEB64_Ubuntu24_Rev29.zip" # Nombre del paquete principal
    "sfd_InstaladorCertificadosCA_Rev16.exe" # Certificados
    "agentegaudi" # Servicio para logearse con firmadigital desde sitios WEB gov.
    "scmanager" # Cambio de PIN en la tarjeta.
)
md5sums=(
    'e2cd864d358caaa90f0939861c399fbc'
    '9686134ebbafc62a6b0c5dcb58e64d8c'
    'e0dd664dae96c518526ad005c051e79d'  # agentegaudi
    '0252f056a209588e3a58d1336f8a32c1'  # scmanager
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
}

package() {
    # Rutas de los .deb dentro del ZIP
    local datadir="${srcdir}/data"
    local debs=(
        "$srcdir/Firma Digital/Idopte/scmiddleware-costa-rica-user_idopte_6.23.44.0_ubun24_amd64.deb"
        "$srcdir/Firma Digital/Agente GAUDI/agente-gaudi_26.0_amd64.deb"
    )
    echo "${debs[0]}" "${debs[1]}"

    # Extraer y copiar los archivos de cada .deb
    install -d "${srcdir}/firmadigital"
    for deb in "${debs[@]}"; do

        printf "${deb}\n"
        debname=$(basename "${deb/.deb/}")
        install -d "${srcdir}/debs/${debname}"
        bsdtar -xf "$deb" -C "$srcdir/debs/$debname"

        if [ -f "$srcdir/debs/$debname/data.tar.xz" ]; then
            tar -xvf "$srcdir/debs/$debname/data.tar.xz" -C "$srcdir/firmadigital"
        elif [ -f "$srcdir/debs/$debname/data.tar.zst" ]; then
            tar -xvf "$srcdir/debs/$debname/data.tar.zst" -C "$srcdir/firmadigital"
        elif [ -f "$srcdir/debs/$debname/data.tar.gz" ]; then
            tar -xvzf "$srcdir/debs/$debname/data.tar.gz" -C "$srcdir/firmadigital"
        else
            ## There is no data.tar.*
            printf "ERROR Processing: ${deb}\n"
            exit 1
        fi
    done

    ## Quitar permisos 777 a algunos ejecutables y archivos ya que es un hueco de seguridad
    find "${srcdir}/firmadigital/" -perm -0077 -exec chmod go-w {} +

    ## Mover todos los certificados
    find $srcdir -type f \( -iname "*.cer" -o -iname "*.crt" \) | \
        while read cert
        do
            # Remover acentos y caracteres extraños
            certname=$( basename "${cert}" | sed 'y/ÁÉÍÓÚÜÑáéíóúüñ/AEIOUUNaeiouun/' |
                            tr '[:upper:]' '[:lower:]' |
                            tr -s ' \-()\t' '_'
                    )
            # echo $certname $( md5sum "$cert" | cut -f 1 -d ' ' )
            if [ -f "${srcdir}/firmadigital/usr/share/ca-certificates/trust-source/anchors/firmadigitalcr/${certname}" ]; then : ;
            else
                   install -Dm644 "${cert}" "${srcdir}/firmadigital/usr/share/ca-certificates/trust-source/anchors/firmadigitalcr/${certname}"
            fi
        done

    ## Crea el directorio de ejecutables
    install -d -m 755 "${srcdir}/firmadigital/usr/bin"

    # Crear el enlace simbólico a Agente-GAUDI
    install -D -m 755 "${srcdir}/agentegaudi" "${srcdir}/firmadigital/usr/bin"

    # Crear el enlace simbólico a SCManager
    install -D -m 755 "${srcdir}/scmanager" "${srcdir}/firmadigital/usr/bin"

    ## Quitar init.d
    rm -r "${srcdir}/firmadigital/etc/init.d"

    ## Usar runtime del sistema
    #rm -r "${srcdir}/firmadigital/opt/Agente-GAUDI/lib/runtime"
    #ln -sf /usr/lib/jvm/java-17-openjdk "${srcdir}/firmadigital/opt/Agente-GAUDI/lib/runtime"

    ## Desktop file
    sed -i 's|Exec=/opt/Agente-GAUDI.*|Exec=/usr/bin/agentegaudi|' "${srcdir}/firmadigital/opt/Agente-GAUDI/lib/Agente-GAUDI.desktop"
    install -D -m 644 "${srcdir}/firmadigital/opt/Agente-GAUDI/lib/Agente-GAUDI.desktop" "${srcdir}/firmadigital/usr/share/applications/Agente-GAUDI.desktop"
    rm "${srcdir}/firmadigital/opt/Agente-GAUDI/lib/Agente-GAUDI.desktop"

    ## Mover los archivos de firmadigital al pkgdir
    cp -r "${srcdir}/firmadigital/"* "${pkgdir}"
}
