# Paquete de Arch Linux FirmaDigital Costa Rica

Este repositorio contiene un script que facilita la instalación del software de firma digital en sistemas basados en Arch. Ten en cuenta que el software en sí **no se proporciona oficialmente aquí**, pero este script está diseñado para ayudar a automatizar el proceso de instalación.

## Descarga del Archivo Requerido

Para utilizar este script, deberás descargar manualmente el archivo `sfd_ClientesLinux_DEB64_\*Rev\*.zip`. Este archivo solo está disponible para usuarios de **Firmadigital**.

Puedes descargar el archivo ZIP desde el siguiente enlace:

[Descargar sfd_ClientesLinux_DEB64_Rev26.zip](https://soportefirmadigital.com/sfdj/dl.aspx?lang=es)

**Importante**: Debes ser un usuario registrado de **Firmadigital** para acceder a este enlace de descarga. La descarga es **manual** y no se proporciona a través de este repositorio.

## Descargo de Responsabilidad

- El software en este repositorio **no es oficial** y se proporciona tal cual.
- Este script tiene como objetivo **simplificar** la instalación del software cliente de **Firmadigital** en sistemas basados en Arch Linux.
- Al usar este script, aceptas la responsabilidad de cumplir con los términos de licencia y uso proporcionados por **Firmadigital**.

## Cómo Usarlo

1. Descarga el archivo `sfd_ClientesLinux_DEB64_Ubutu24_Rev27.zip` desde el enlace proporcionado arriba.
2. Coloca el archivo ZIP en el mismo directorio que el script o especifica la ruta correcta en el `PKGBUILD`.
3. Sigue las instrucciones en el `PKGBUILD` para compilar e instalar el paquete.

Una vez que la dependencia esté descargada, puedes ejecutar los siguientes comandos en el directorio del script:
```bash
makepkg
sudo pacman -U firmadigital-26-1-x86_64.pkg.tar.zst
```
No olvides habilitar e iniciar el servicio **pcscd**, que es necesario para la comunicación con el lector de tarjetas.
```bash
sudo systemctl enable --now pcscd
sudo systemctl start pcscd
```

Para utilizar el **Agente-GAUDI**, ejecuta el siguiente comando en la terminal:
```bash
agentegaudi
```

Para más información, consulta la documentación oficial de **Firmadigital**.

## Licencia

El software y el script se proporcionan bajo los términos de una **licencia personalizada**. Consulta los términos de licencia específicos del software que se está instalando.
