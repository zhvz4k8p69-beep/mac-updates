# mac-updates

Public host for the Sparkle update feeds and signed release archives of Dom's
private macOS apps. Source code lives in separate private repositories; only
notarized builds and their appcasts are published here.

| App | Feed (permanent, in the `updates` release) | Release tag pattern |
|-----|--------------------------------------------|---------------------|
| BettWatch | `releases/download/updates/BettWatch-appcast.xml` | `BettWatch-v<version>` |
| BettMoney | `releases/download/updates/BettMoney-appcast.xml` | `BettMoney-v<version>` |

Each app's feed URL is baked into its `Info.plist` (`SUFeedURL`); never rename or
move a feed asset. Versioned releases are immutable: upload the zip, then replace
the feed asset in `updates` with `gh release upload updates <appcast> --clobber`.
Enclosures are verified with each app's own Ed25519 key (`SUPublicEDKey`), so a
file in this repo cannot be swapped for an unsigned build.
