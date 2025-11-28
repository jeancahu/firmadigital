# Información técnica para instalación MANUAL y LOCAL de FirmaDigital Costa Rica en sistema Arch Linux

![Arch Linux](https://img.shields.io/badge/Arch%20Linux-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![Manjaro](https://img.shields.io/badge/Manjaro-34BE5B?style=for-the-badge&logo=manjaro&logoColor=white)
![EndeavourOS](https://img.shields.io/badge/EndeavourOS-7F7FFF?style=for-the-badge&logo=endeavouros&logoColor=white)
![SteamOS](https://img.shields.io/badge/SteamOS-000000?style=for-the-badge&logo=steam&logoColor=white)
![pacman](https://img.shields.io/badge/pacman-FBD000?style=for-the-badge&logo=arch-linux&logoColor=black)
![One Command Install](https://img.shields.io/badge/install-one--command-success?style=for-the-badge&logo=console)
![License: Custom](https://img.shields.io/badge/License-Custom-lightgrey?style=for-the-badge)

Este repositorio contiene la regla necesaria para instalación del paquete oficial del software de firma digital en formato Debian para sistemas basados en Arch. Ten en cuenta que el software en sí **no se proporciona en este repositorio**.

## Descarga el paquete oficial de Ubuntu

Para utilizar este script, deberás descargar **manualmente** el archivo `sfd_ClientesLinux_DEB64.zip` el cual contiene el software en cuestión. Este comprimido solo está disponible para usuarios *Autorizados* de **Firmadigital** y no se encuentra en este repositorio.

Puedes descargar el archivo ZIP desde el siguiente enlace:

[Consultar en el sitio oficial de Soporte Firma Digital](https://soportefirmadigital.com/)

**Importante**: Debes ser un usuario registrado de **Firmadigital** para realizar la descarga de forma **manual**.

## Descargo de Responsabilidad / DISCLAIMER

Este repositorio únicamente proporciona herramientas técnicas (como PKGBUILD, scripts o instrucciones)
para facilitar la instalación del software "Agente GAUDI" en sistemas basados en Arch Linux
mediante los paquetes oficiales (.deb) publicados por el Banco Central de Costa Rica (BCCR).

### IMPORTANTE:

- Este repositorio NO incluye, distribuye, contiene ni almacena ningún archivo binario,
  fragmento, componente, biblioteca, código fuente, documentación o recurso perteneciente
  al software Agente GAUDI o al Banco Central de Costa Rica.
- Los archivos necesarios para la instalación (incluyendo el paquete .deb oficial)
  deben ser descargados directamente por el usuario desde las fuentes oficiales del BCCR o FirmaDigital.
- El uso del software Agente GAUDI está sujeto a la licencia de usuario final emitida por
  el Banco Central de Costa Rica. Este repositorio NO modifica, altera, parchea,
  adapta, descompila ni ejecuta ingeniería inversa sobre el software.
- El script o PKGBUILD proporcionado es únicamente una herramienta auxiliar y opcional.
  Su uso no exime al usuario de leer, aceptar y cumplir estrictamente la licencia oficial
  del software Agente GAUDI antes de instalarlo o utilizarlo.
- El autor de este repositorio no se responsabiliza por el uso indebido del software,
  incumplimiento de la licencia del BCCR, posibles daños derivados de la instalación o uso,
  ni por cualquier acción que contravenga la legislación vigente o los términos de licencia.
> ❗Si usted no está autorizado por el BCCR para usar el software Agente GAUDI en su sistema, o no ha aceptado expresamente los términos de su licencia, debe abstenerse de utilizar el contenido de este repositorio.
- Este proyecto se proporciona tal cual es de carácter educativo/técnico/personal
  y no está afiliado, asociado, respaldado, aprobado ni supervisado por el Banco Central de Costa Rica.
- La regla de empaquetado es OpenSource por lo que puede someterse al escrutinio público, la misma
  describe procesos estandarizados para el empaquetado y posterior instalación de software en
  sistemas operativos basados en ArchLinux.

Al utilizar los scripts aquí contenidos, usted asume toda la responsabilidad por su uso y
declara aceptar los términos anteriores, así como cumplir con los términos de licencia y
uso proporcionados por **Firmadigital**.

## Cómo Usarlo

1. Descarga el archivo `sfd_ClientesLinux_DEB64_Ubuntu*.zip` desde el enlace proporcionado arriba.
2. Coloca el archivo ZIP en el mismo directorio que el script o especifica la ruta correcta en el `PKGBUILD`.
3. Sigue las instrucciones en el `PKGBUILD` para interpretar e instalar el paquete Debian.

Una vez que la dependencia esté descargada, puedes ejecutar los siguientes comandos en el directorio del script:
```bash
makepkg # Interpretar el paquete oficial en formato Debian para instalación en ArchLinux
sudo pacman -U firmadigital-VERSION-x86_64.pkg.tar.zst # Instalar el paquete
rm firmadigital-VERSION-x86_64.pkg.tar.zst # Borrar el archivo temporal de instalación
```
No olvides habilitar e iniciar el servicio **pcscd**, que es necesario para la comunicación con el lector de tarjetas.
```bash
sudo systemctl enable --now pcscd
```

Para utilizar el **Agente-GAUDI**, ejecuta el siguiente comando en la terminal:
```bash
agentegaudi
```

Para utilizar el **SCManager**, ejecuta el siguiente comando en la terminal:
```bash
scmanager
```

Para más información, consulte la documentación oficial.

## Licencia

El software y el script se proporcionan bajo los términos de una **licencia personalizada**.
Consulta los términos de licencia específicos del software que se está instalando.
