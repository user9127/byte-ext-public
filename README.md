# byte-ext-public

Public distribution for **Byte External** — launcher, installer, and UI package.

Downloads are published as GitHub Releases (`v<version>` tag) with these artifacts:

| Artifact | Role |
| --- | --- |
| `ByteExtInstaller.exe` | One-time installer. Installs to `%LOCALAPPDATA%\ByteExternal`, downloads the current launcher, UI, and payload, verifies SHA-256, creates shortcuts, and installs the WebView2 runtime if missing. Reusable across future releases — no rebuild needed. |
| `ByteExternalLauncher.exe` | Launcher. WebView2 host, key / login / register / settings / community UI. Handles auth against byte-license and spawns the payload with a one-shot launch token. Auto-updates itself, the UI, and the payload against `https://api.projectbyte.cc/version`. |
| `ByteExternal.exe` | Payload. The actual external Roblox companion. Refuses to run without `--launch-token=…` — launch via the launcher. |
| `byte-external-ui-<version>.zip` | UI package. HTML/CSS/JS the launcher serves to its embedded WebView2. Versioned filename so caches don't lie. |
| `SHA256SUMS` | Checksums for the four files above. |

The authoritative version metadata lives in `https://api.projectbyte.cc/version` — see fields `external_version`, `launcher_url`, `external_url`, `ui_url`, and the matching `*_sha256`s. The installer and the launcher both fetch that manifest at runtime; no URL or hash is baked in.

## Downloads

The latest release is tagged **v1.0.0**:

- https://github.com/user9127/byte-ext-public/releases/latest

Users typically only need `ByteExtInstaller.exe`.

## Verifying a download

```powershell
Get-FileHash .\ByteExtInstaller.exe -Algorithm SHA256
```

Compare the hash to the matching line in `SHA256SUMS` or in the `api.projectbyte.cc/version` manifest.

## Source

Launcher, installer, UI, and payload source live in the private `byte-private` repository under `byte-external/` and `byte-ext-build/`. This repository hosts the built binaries only.

## Community

Discord: https://discord.gg/xbyte &middot; Website: https://projectbyte.cc
