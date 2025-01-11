# ArchLinux Package FirmaDigital Costa Rica

This repository contains a script that facilitates the installation of the digital signature software on Arch-based systems. Please note that the software itself is not officially provided here, but this script is designed to help automate the installation process.

## Downloading the Required File

To use this script, you will need to download the `sfd_ClientesLinux_DEB64_Rev26.zip` file manually. This file is only available to **Firmadigital** users.

You can download the ZIP file from the following link:

[Download sfd_ClientesLinux_DEB64_Rev26.zip](https://soportefirmadigital.com/sfdj/dl.aspx?lang=es)

**Important**: You must be a registered user of **Firmadigital** to access this download link. The download is **manual** and not provided through this repository.

## Disclaimer

- The software in this repository is **not official** and is provided as-is.
- This script is intended to **simplify** the installation of the **Firmadigital** client software on Arch Linux-based systems.
- By using this script, you accept the responsibility of ensuring compliance with any licensing or usage terms provided by **Firmadigital**.

## How to Use

1. Download the `sfd_ClientesLinux_DEB64_Rev26.zip` file from the link provided above.
2. Place the ZIP file in the same directory as the script or specify the correct path in the `PKGBUILD`.
3. Follow the instructions in the `PKGBUILD` to build and install the package.

Once the dependency is downloaded, you can run the following commands in the directory of the script:
```bash
makepkg
sudo pacman -U firmadigital-26-1-x86_64.pkg.tar.zst
```
Don't forget to enable and start the **pcscd** service, which is required to communicate with the card reader.
```bash
sudo systemctl enable --now pcscd
sudo systemctl start pcscd
```

To use the **Agente-GAUDI**, run the following command in the terminal:
```bash
agentegaudi
```

For more information, please refer to the official documentation from **Firmadigital**.

## License

The software and script are provided under the terms of **custom license**. Please refer to the individual licensing terms of the software being installed.
