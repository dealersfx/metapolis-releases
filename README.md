# METApolis Photo Lab — Windows Downloads

**Developed by DealersFX**

This is the official **public distribution repository** for **METApolis Photo Lab for Windows**. It is intended for **installer downloads, version announcements, and signed update metadata only**.

> **Release status:** The first Windows installer has not yet been built, tested, or published. There is currently no official setup EXE to download.

## Download

Once the initial Windows installer is released, download it from [GitHub Releases](https://github.com/dealersfx/metapolis-releases/releases). A public release may be downloaded by anyone; possession of an installer does not imply exclusive access.

## Updates

All users share **one release channel** (no separate beta channel). The application can check the following stable location for newer versions:

`https://raw.githubusercontent.com/dealersfx/metapolis-releases/main/latest.json`

**That manifest is intentionally absent until the first verified release.** It must be signed with the distributor's offline Ed25519 private key and must reference an already published, tested Windows installer. The application verifies the manifest's signature and the installer SHA-256 and size before an update can be installed.

Updates are optional. Editing works offline, and optional AI is not required for manual editing.

## Privacy and source code

- **Source code is not published in this repository.** It is maintained separately and privately.
- Release-signing private keys, project sources, sample RAW photos, catalogs, layers, masks, presets and user data **must never be committed here**.
- The application's photo catalog and edits remain on the user's device and are not uploaded through update checking.
- GitHub Releases assets hosted here are public, even if the application source code remains private.

## Release procedure

See [RELEASE_PROCESS.md](RELEASE_PROCESS.md) for the publisher's checklist, including the Windows test/approval gate and the requirement to publish the signed manifest **last**.

## Rights

Publicly available binary downloads do **not** mean that this repository is open-source. No open-source license is granted here.
