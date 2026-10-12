# byte-ext-public

Public distribution for **Byte External**: installer, launcher and payload.

Downloads are published as GitHub Releases (`v<version>` tag) with these artifacts:

| Artifact | Role |
| --- | --- |
| `ByteExtInstaller.exe` | One-time installer. Installs to `%LOCALAPPDATA%\ByteExternal`, downloads the current launcher and payload, verifies SHA-256, installs the WebView2 Runtime if missing, creates shortcuts and an Apps entry with an uninstaller. Reusable across future releases, no rebuild needed. |
| `ByteExternalLauncher.exe` | Launcher. WebView2 window with its UI built into the exe (sign in, license key, create account, launch, settings, controls). Signs in against byte-license and starts the payload with a one-shot launch token. Updates itself and the payload from `https://api.projectbyte.cc/version`. |
| `ByteExternal.exe` | Payload. The external Roblox companion. Refuses to run without `--launch-token=...`, so start it from the launcher. |
| `SHA256SUMS` | Checksums for the three files above. |

Since 1.0.1 the launcher UI ships inside `ByteExternalLauncher.exe`, so there is no separate UI zip. The 1.0.0 release still carries `byte-external-ui-1.0.0.zip` for launchers that were installed with it.

The authoritative version metadata lives in `https://api.projectbyte.cc/version` (fields `external_version`, `launcher_version`, `external_url`, `launcher_url` and the matching `*_sha256`). The installer and the launcher both fetch it at runtime; no URL or hash is baked in.

## Downloads

The latest release is tagged **v1.0.1**:

- https://github.com/user9127/byte-ext-public/releases/latest

Users only need `ByteExtInstaller.exe`. Anyone still on 1.0.0 should run the new installer once; the 1.0.0 launcher can't replace itself.

## Verifying a download

```powershell
Get-FileHash .\ByteExtInstaller.exe -Algorithm SHA256
```

Compare the hash to the matching line in `SHA256SUMS` or in the `api.projectbyte.cc/version` manifest.

## Source

Launcher, installer and payload source live in the private `byte-private` repository under `byte-ext-build/` and `byte-external/`. This repository hosts the built binaries only.

## Community

Discord: https://discord.gg/xbyte &middot; Website: https://projectbyte.cc
