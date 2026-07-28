# Helium .xbps

Helium web browser packaged as `.xbps` for **Void Linux**.

## What is Helium?

[Helium](https://helium.computer/) is a privacy-first, Chromium-based web browser with unbiased ad-blocking. No bloat, no noise.

## How it works

This repo runs a weekly GitHub Action that:

1. Fetches the latest `.deb` from [imputnet/helium-linux](https://github.com/imputnet/helium-linux/releases)
2. Strips bloat — removes chromedriver, debug `.info` files, non-English locales (~137 MB saved uncompressed)
3. Repackages as a native `.xbps` with proper INSTALL/REMOVE scripts
4. Publishes a GitHub Release with the `.xbps` attached

## Install

Download the latest `.xbps` from [Releases](https://github.com/Ars-byte/Helium_xbps/releases) and install:

```sh
sudo xbps-install -y ./helium-bin-*.x86_64.xbps
```

Or add the repo:

```sh
# TODO: hosted repo URL
```

## Build locally

On a Void Linux machine:

```sh
git clone https://github.com/Ars-byte/Helium_xbps.git
cd Helium_xbps
chmod +x build-helium-xbps.sh
./build-helium-xbps.sh
```

Requires: `curl`, `jq`, `binutils`, `xbps`

## Size optimizations

| Removed          | Uncompressed | Reason                        |
|------------------|-------------|-------------------------------|
| chromedriver     | ~21 MB      | WebDriver for automation      |
| `*.info` files   | ~65 MB      | Debug metadata (.pak.info)   |
| i18n locales     | ~45 MB      | Only `en-US` kept             |
| **Total saved**  | **~137 MB** | —                             |

## License

Helium is GPL-3.0. The packaging scripts in this repo are MIT.
