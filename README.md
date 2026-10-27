# METApolis Photo Lab — Windows Downloads

**Developed by DealersFX**

This is the official **public distribution repository** for **METApolis Photo Lab for Windows**. It is intended for **installer downloads, version announcements, and signed update metadata only**.

> **Release status:** **v1.0.0 is published** as a public Windows release. The installer asset checksum and size match the signed update manifest. Further user acceptance testing of the Windows GUI and 16-bit export should continue after publication.

## Download

Download [METApolis Photo Lab v1.0.0 for Windows](https://github.com/dealersfx/metapolis-releases/releases/tag/v1.0.0), or browse [all releases](https://github.com/dealersfx/metapolis-releases/releases). A public release may be downloaded by anyone; possession of an installer does not imply exclusive access.

## Updates

All users share **one release channel** (no separate beta channel). The application can check the following stable location for newer versions:

`https://raw.githubusercontent.com/dealersfx/metapolis-releases/main/latest.json`

**The signed manifest is now published.** The application checks the Ed25519 signature before trusting the release URL, and checks the installer SHA-256 and size before installing an update. Installed v1.0.0 copies are already current and therefore should report that no newer update is available. Future releases must publish the installer asset **before** updating this signed manifest.

Updates are optional. Editing works offline, and optional AI is not required for manual editing.

## Privacy and source code

- **Source code is not published in this repository.** It is maintained separately and privately.
- Release-signing private keys, project sources, sample RAW photos, catalogs, layers, masks, presets and user data **must never be committed here**.
- The application's photo catalog and edits remain on the user's device and are not uploaded through update checking.
- GitHub Releases assets hosted here are public, even if the application source code remains private.
- The update manifest is signed with Ed25519. This is not the same as Windows Authenticode signing of the installer; Windows may show an unsigned-app warning.

## Release procedure

See [RELEASE_PROCESS.md](RELEASE_PROCESS.md) for the publisher's checklist, including the Windows test/approval gate and the requirement to publish the signed manifest **last**.

## Rights

Publicly available binary downloads do **not** mean that this repository is open-source. No open-source license is granted here.
