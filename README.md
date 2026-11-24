# PoundControl-Plugins

The official curated plugin catalog for [PoundControl](https://github.com/mrpoundsign/PoundControl).

- **Live Catalog URL**: `https://raw.githubusercontent.com/mrpoundsign/PoundControl-Plugins/main/catalog.json`

## Catalog Format (`catalog.json`)

The catalog root is a JSON object with `version` (`1`) and a `plugins` array.

### Entry Fields

| Field | Required | Description |
| :--- | :--- | :--- |
| `id` | Yes | Unique reverse-DNS plugin UUID matching the plugin manifest. |
| `name` | Yes | Display name in PoundControl Studio. |
| `kind` | Yes | `"wasm"` (sandboxed WebAssembly `.wasm` plugin) or `"sdplugin"` (Elgato/OpenAction `.sdPlugin` bundle). |
| `author` | No | Plugin author or organization name. |
| `category` | No | Catalog category (e.g. `"Streaming"`, `"Audio"`, `"Utilities"`). |
| `description` | No | Short summary shown in the Curated Plugins browser. |
| `repository` | Yes* | GitHub repository URL (`https://github.com/<owner>/<repo>`) hosting releases. |
| `assetName` | Yes for `wasm` | Exact release asset filename to download (e.g. `poundcontrol-twitch.wasm`). |
| `download_url` | Optional | Direct HTTPS download URL if not resolving via GitHub Releases. |
| `sha256` | Optional | Expected SHA-256 hex digest when using a direct `download_url`. |
| `icon` | No | HTTPS URL to a `.svg`, `.png`, or `.jpg` icon. |
| `allowedHosts` | Recommended for `wasm` | List of HTTP hosts declared in the Wasm plugin sandbox manifest, displayed to users before installation. |
| `featured` | No | When `true`, sorts the entry to the top of the curated catalog. |
| `minAppVersion` | No | Minimum recommended PoundControl version. |

## Release & Checksum Expectations

For GitHub Release-hosted plugins, PoundControl downloads release assets using `appinstaller/pkg/updater` and **requires** SHA-256 verification against a `checksums.txt` or `SHA256SUMS.txt` file attached to the release:

```text
<64-hex-sha256>  poundcontrol-twitch.wasm
```

Releases for `.sdPlugin` bundles may attach `.streamDeckPlugin` or `.zip` assets (with optional GitHub asset digest or `checksums.txt`).
