# Arx engine archives

This repository holds the prebuilt engine of [Arx](https://github.com/capturecontext/arx-browser), a web browser for macOS. It has no source code: every engine is a [release](https://github.com/capturecontext/arx-browser-engine/releases) here, and the archives are its assets.

The engine is [Helium](https://github.com/imputnet/helium), a privacy-focused Chromium by imput, built with Arx's own patches into an embeddable framework, `Arx Framework.framework`. Building it is a full Chromium build that takes hours, so Arx's build downloads it from here instead.

## Where the source is

All of it is in [`capturecontext/arx-browser`](https://github.com/capturecontext/arx-browser):

- `Packages/engine/engine.lock.json` pins the helium-macos, Helium and Chromium revisions.
- `Scripts/engine` has Arx's changes to Chromium, as overlays, and the build commands.
- `Packages/engine/Native` has the native code compiled into Chromium.

To build an engine yourself, follow [The engine](https://github.com/capturecontext/arx-browser#the-engine) in that repository's README.

## Releases

Each release is one engine, tagged `engine-<first 16 hex digits of its source fingerprint>`. The fingerprint is computed from the engine's sources in `arx-browser`, so one tag never names two different engines. Each architecture is one asset:

```text
https://github.com/capturecontext/arx-browser-engine/releases/download/engine-<fingerprint>/arx-engine-macos-<architecture>.tar.gz
```

The archives are for Apple silicon (`arm64`) and macOS 27 or later. They are development artifacts, not a notarized app.

To find the source of a release, look for the commit of `arx-browser` whose `Artifacts/Engine/arx-engine-macos-<architecture>.json` names that release's URL. The manifest also records the full fingerprint, the Chromium version, and the archive's size and SHA-256.

## Using an archive

You don't download these by hand. In a clone of `arx-browser`:

```sh
make engine-fetch engine-validate
```

`make engine-fetch` reads the manifest, downloads the archive it names, and checks its size and SHA-256 before unpacking anything. [Artifacts/Engine](https://github.com/capturecontext/arx-browser/blob/main/Artifacts/Engine/README.md) in `arx-browser` describes the rest, including how a new engine is published.

## Licence

The engine is free software under the GNU General Public License, version 3: see [LICENSE](LICENSE). It contains Helium, under the same licence, and Chromium and ungoogled-chromium code under the BSD 3-Clause License: see [LICENSE.ungoogled_chromium](LICENSE.ungoogled_chromium). `arx-browser`'s `THIRD_PARTY_NOTICES.md` lists every dependency and its licence.

Report problems in [`arx-browser`'s issues](https://github.com/capturecontext/arx-browser/issues), not here.
