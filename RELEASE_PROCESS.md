# METApolis Photo Lab — Release publication checklist

**Distribution:** Public installers, private source code. **Channels:** One.

This repository contains **only** release documentation, signed update metadata (`latest.json` when activated) and release assets. Never upload the application source ZIP, a full project folder, photos, edit catalogs, masks, private keys or credentials.

## Before publishing the first release

1. Build the installer **on Windows x64** from the **private** METApolis Photo Lab source repository/project, using Python 3.12, PyInstaller and Inno Setup 6.
2. Generate an Ed25519 signing key **on the release owner's trusted PC**, outside the source directory. Protect and back it up; do not upload it or transmit it in chat.
3. Embed the *public* Ed25519 key and this constant manifest URL into the Windows build:
   `https://raw.githubusercontent.com/dealersfx/metapolis-releases/main/latest.json`
4. Run the application's regression tests and test the built installer on a clean Windows system. Check startup, RAW decoding, Develop tools, masks and layers, project Save/Reopen, JPEG/PNG/TIFF exports, uninstall, and preservation of user data.
5. Test an in-place upgrade with the **same Inno Setup AppId**. Confirm the installed application still functions offline.
6. Do **not** publish a test-only build with `-AllowUnconfiguredUpdates` as the official installer.

## Build (private source folder only)

```powershell
py -3.12 -m pip install cryptography
py -3.12 installer/release_keys.py --private-key "$env:USERPROFILE\Documents\METApolis-release-secret\signing.pem"

powershell -ExecutionPolicy Bypass -File .\installer\build_windows.ps1 `
  -ManifestUrl "https://raw.githubusercontent.com/dealersfx/metapolis-releases/main/latest.json" `
  -PublicKeyBase64 "PUBLIC_KEY_PRINTED_BY_RELEASE_KEYS"
```

The private signing key must **not** be committed anywhere. Its *public* key is safe to embed in the installer.

Expected first output after successful Windows compilation:

`artifacts/METApolis_Photo_Lab_v1.0.0_Setup.exe`

## Publish (only after the installer passes Windows acceptance)

Install Git and GitHub CLI, run `gh auth login` as the repository publisher, then from the **private source** folder:

```powershell
powershell -ExecutionPolicy Bypass -File .\installer\publish_public_release.ps1 `
  -Installer ".\artifacts\METApolis_Photo_Lab_v1.0.0_Setup.exe" `
  -PrivateKey "$env:USERPROFILE\Documents\METApolis-release-secret\signing.pem" `
  -Version "1.0.0" `
  -Notes "Initial Windows release"
```

The publisher script must:
1. Publish the **EXE only** as a GitHub Release tagged `v1.0.0`.
2. Generate a signed `latest.json` containing the exact release asset HTTPS URL, installer version, SHA-256 and size.
3. Commit that signed `latest.json` to this repository **last**, after the EXE is publicly available.

Until these steps are completed, **there must be no `latest.json`**: an unsigned or fake feed is worse than an absent feed.

## For every subsequent version

1. Advance `APP_VERSION` in the private source and build/test the new installer.
2. Keep the same AppId, manifest URL, and pinned signing public key.
3. Publish a new immutable release tag and the finished installer, then update signed `latest.json` last.
4. Open the manifest and release asset URL in a private/incognito browser; verify an installed older version prompts for the update.
5. Keep original installers for rollback. Do not reuse release version numbers or silently replace existing binaries.

## Security and operating notes

- Public GitHub Releases are **downloadable by anyone**. A private source repository remains private.
- Ed25519 manifest signatures authenticate our update feed; file size and SHA-256 protect download integrity. These are **not** Windows Authenticode signatures. For wider distribution, digitally sign the Windows executable and installer as well.
- An already distributed version cannot receive updates if the embedded manifest URL or signing key is changed without a compatible migration process.
- Do not make a public repo private without first moving installed clients to a new reachable update feed.
- Users' photos, edits and settings are stored outside the installation directory and must remain untouched by upgrades and uninstallation.

**Current status:** Public GitHub distribution repository configured; the Windows installer has **not** been built or published.
