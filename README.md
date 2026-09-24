# mac-updates

Public host for the Sparkle update feeds and signed release archives of Dom's
private macOS apps. Source code lives in separate private repositories; only
notarized builds and their appcasts are published here.

| App | Feed (permanent, in the `updates` release) | Release tag pattern |
|-----|--------------------------------------------|---------------------|
| BettWatch | `releases/download/updates/BettWatch-appcast.xml` | `BettWatch-v<marketing>-<build>` |
| BettMoney | `releases/download/updates/BettMoney-appcast.xml` | `BettMoney-v<marketing>-<build>` |
| Ready Room | `releases/download/updates/ReadyRoom-appcast.xml` | `ReadyRoom-v<marketing>-<build>` |
| TroopLedger | `releases/download/updates/TroopLedger-appcast.xml` | `TroopLedger-v<marketing>-<build>` |
| Foley | `releases/download/updates/Foley-appcast.xml` | `Foley-v<marketing>-<build>` |

Each app's feed URL is baked into its `Info.plist` (`SUFeedURL`); never rename or
move a feed asset. Versioned releases are immutable: upload the zip, then replace
the feed asset in `updates` with `gh release upload updates <appcast> --clobber`.
Enclosures are verified with each app's own Ed25519 key (`SUPublicEDKey`), so a
file in this repo cannot be swapped for an unsigned build.

Publishing is done by each app's `prepare-sparkle-update.sh --publish`, which
creates the versioned release, waits until the zip downloads anonymously, and
only then replaces the feed asset.
