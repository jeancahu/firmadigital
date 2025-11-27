# Manual and Local installation for ArchLinux Package on FirmaDigital Costa Rica

[README Español](./README_es.md)

This repository provides a *packaging rule (PKGBUILD)* that helps convert the official digital signature software package (distributed in Debian format) for use on Arch Linux-based systems.
Please note that **the software itself is NOT provided in this repository**

## Downloading the Debian formatted package

To use this script, you will need to download the `sfd_ClientesLinux_DEB64_\*_Rev\*.zip` file manually. This file is only available to **Firmadigital** users.

You can download the ZIP file from the following link:
- [FirmaDigital Official WebSite](https://soportefirmadigital.com/)

**Important**: You must be a registered user of **Firmadigital** to access to the resource URL. Required package is **manually downloadable** and not provided through this repository.

---

## Legal Disclaimer

This repository only provides technical tools (such as `PKGBUILD`, scripts, or installation instructions)
to assist in installing the **“Agente GAUDI”** software on Arch Linux-based systems, by converting from the
official `.deb` packages published by the **Banco Central de Costa Rica (BCCR)**.

### IMPORTANT NOTES

- This repository **does NOT include, distribute, store, or contain ANY binary file, code fragment, component, library, documentation, or intellectual property** from the Agente GAUDI software or the BCCR.
- All required installation files (including the official `.deb` package) must be downloaded **directly** from the official BCCR or FirmaDigital sources by the user.
- The use of Agente GAUDI is strictly subject to the **End-User License Agreement (EULA)** issued by the BCCR.
- This repository does **not** modify, alter, patch, reverse engineer, adapt, repackage, or otherwise manipulate the official software.
- The provided script/PKGBUILD is an *optional technical helper only*. Using it does **not** exempt the user from reading, accepting, and fully complying with the official license agreement of Agente GAUDI **before installing or using it**.
- The repository author assumes **no responsibility** for improper use, license violation, direct or indirect damages, legal consequences, or any misuse of the software.

> ❗ If you are not authorized by the BCCR to use Agente GAUDI, or have not explicitly accepted its license terms, you must **not** use this repository.

This project is provided *as-is*, for purely educational/technical/personal purposes, and **is not affiliated with, endorsed by, approved by, or supervised by the Banco Central de Costa Rica**.

The packaging rule is **open-source** and publicly reviewable. It describes standardized procedures for packaging and installation of software on Arch Linux-based operating systems.

By using any script contained in this repository, you acknowledge full responsibility and agree to comply with all related licensing and usage terms provided by **FirmaDigital** and the **BCCR**.

---
## How to Use

1. Download the `sfd_ClientesLinux_DEB64_Ubuntu_YOUR_DOWNLOADED_VERSION.zip` file from the link provided above.
2. Place the ZIP file in the same directory as the script or specify the correct path in the `PKGBUILD`.
3. Follow the instructions in the `PKGBUILD` to build and install the package.

Once the dependency is downloaded, you can run the following commands in the directory of the script:
```bash
makepkg
sudo pacman -U firmadigital-VERSION-x86_64.pkg.tar.zst
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

For **SCManager** execution type the following command:
```bash
scmanager
```

More information about the software itself on the
**[FirmaDigital Official Documentation](https://soportefirmadigital.com/)**.


## License

The software and script are provided under the terms of **custom license**. Please refer to the individual licensing terms of the software being installed.
