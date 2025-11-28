# Instructions for FirmaDigital Costa Rica Manual installation on ArchLinux

![Arch Linux](https://img.shields.io/badge/Arch%20Linux-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![Manjaro](https://img.shields.io/badge/Manjaro-34BE5B?style=for-the-badge&logo=manjaro&logoColor=white)
![EndeavourOS](https://img.shields.io/badge/EndeavourOS-7F7FFF?style=for-the-badge&logo=endeavouros&logoColor=white)
![SteamOS](https://img.shields.io/badge/SteamOS-000000?style=for-the-badge&logo=steam&logoColor=white)
![pacman](https://img.shields.io/badge/pacman-FBD000?style=for-the-badge&logo=arch-linux&logoColor=black)
![One Command Install](https://img.shields.io/badge/install-one--command-success?style=for-the-badge&logo=console)
![License: Custom](https://img.shields.io/badge/License-Custom-lightgrey?style=for-the-badge)

[README Español](./README_es.md)

This repository provides a *packaging rule (PKGBUILD)* that helps install the official **Firmadigital** software package (distributed in Debian format) for use on Arch Linux-based systems.
Please note that **the software itself is NOT provided in this repository**

## Downloading the Debian formatted package

To use this script, you will need to download the `sfd_ClientesLinux_DEB64_\*_Rev\*.zip` file manually. This file is only available to **Firmadigital** users.

You can download the ZIP file from the following link:
- [FirmaDigital Official WebSite](https://soportefirmadigital.com/)

**Important**: You must be a registered user of **Firmadigital** to access to the resource URL. Required package is **manually downloadable** and not provided through this repository.

---

## Legal Disclaimer

This repository only provides technical tools (such as `PKGBUILD`, scripts, or installation instructions)
to assist in installing the **“Agente GAUDI”** software on Arch Linux-based systems, from the
official `.deb` packages published by the **Banco Central de Costa Rica (BCCR)**.

### IMPORTANT NOTES

- This repository **does NOT include, distribute, store, or contain ANY binary file, code fragment, component, library, documentation, or intellectual property** from the Agente GAUDI software or the BCCR.
- All required installation files (including the official `.deb` package) must be downloaded **directly** from the official BCCR or FirmaDigital sources by the user.
- The use of Agente GAUDI is strictly subject to the **End-User License Agreement (EULA)** issued by the BCCR.
- This repository does **not** modify, alter, patch, reverse engineer, adapt, or otherwise manipulate the official software.
- The provided script/PKGBUILD is an *optional technical helper only*. Using it does **not** exempt the user from reading, accepting, and fully complying with the official license agreement of Agente GAUDI **before installing or using it**.
- The repository author assumes **no responsibility** for improper use, license violation, direct or indirect damages, legal consequences, or any misuse of the software.

> ❗ If you are not authorized by the BCCR to use Agente GAUDI, or have not explicitly accepted its license terms, you must **not** use this repository.

This project is provided *as-is*, for purely educational/technical/personal purposes, and **is not affiliated with, endorsed by, approved by, or supervised by the Banco Central de Costa Rica**.

The packaging rule is **open-source** and publicly reviewable. It describes standardized procedures for packaging and installation of software on Arch Linux-based operating systems.

By using any script contained in this repository, you acknowledge full responsibility and agree to comply with all related licensing and usage terms provided by **FirmaDigital** and the **BCCR**.

---
## Usage

1. Download the `sfd_ClientesLinux_DEB64_Ubuntu_YOUR_DOWNLOADED_VERSION.zip` file from the link provided above.
2. Place the ZIP file in the same directory as the script or specify the correct path in the `PKGBUILD`.
3. Follow the instructions in the `PKGBUILD` to install the Debian package.

Once the dependency is downloaded, you can run the following commands in the directory of the script:
```bash
makepkg # Consume the official package Debian format for pacman processing
sudo pacman -U firmadigital-VERSION-x86_64.pkg.tar.zst # Install the software
rm firmadigital-VERSION-x86_64.pkg.tar.zst # Remove temporal files once installed the software
```
Don't forget to enable and start the **pcscd** service, which is required to communicate with the card reader.
```bash
sudo systemctl enable --now pcscd
```

To use the **Agente-GAUDI**, run the following command in the terminal:
```bash
agentegaudi
```

For **SCManager** execution type the following command:
```bash
scmanager
```

## License

The software and script are provided under the terms of **custom license**. Please refer to the individual licensing terms of the software being installed.
