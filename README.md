# CaseFlow Desktop — Releases

Public download and auto-update feed for **CaseFlow Desktop**, by
[WebXL Digital Solutions](https://web-xl.com).

## What lives here

Build artifacts only:

| File                                           | Purpose                                        |
| ---------------------------------------------- | ---------------------------------------------- |
| `CaseFlow-Desktop-<version>-universal.dmg`     | macOS installer (Apple Silicon **and** Intel)  |
| `CaseFlow-Desktop-<version>-universal-mac.zip` | macOS auto-update payload                      |
| `CaseFlow-Desktop-<version>-setup.exe`         | Windows x64 installer                          |
| `latest-mac.yml` / `latest.yml`                | `electron-updater` feed metadata               |
| `*.blockmap`                                   | differential-update block maps                 |

**No source code is published here, ever.** The application source lives in a separate private
repository. This repo exists so the shipped app can read its update feed over plain HTTPS without
embedding a GitHub credential — which a private feed would require.

## Verifying a macOS download

Every macOS build is signed with the Developer ID Application certificate of
**Yogev Tuval (Team ID `UZULD5TMGN`)**, notarized by Apple, and stapled — the `.dmg` container
itself, not only the app inside it. To check a download yourself:

```sh
spctl -a -t open --context context:primary-signature -vv "CaseFlow Desktop-<version>-universal.dmg"
# expected: accepted / source=Notarized Developer ID

xcrun stapler validate "CaseFlow Desktop-<version>-universal.dmg"
# expected: The validate action worked!
```

The `sha512` recorded in `latest-mac.yml` is computed from the **final signed** bytes, so it matches
the file you download. Signing rewrites the container after packaging, so the feed is regenerated
afterwards — precisely so the two can never disagree.

## Support

Issues and feature requests are handled through CaseFlow support, not this repository.
