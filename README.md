# iOS URI Schemes

A community-curated list of iOS apps and games with their associated URL/URI schemes, App Store IDs, bundle identifiers, and IGDB IDs.

This repository is intended as a lightweight, machine-readable reference for developers, shortcut builders, and automation enthusiasts who need to launch or deep-link into iOS apps.

## What's in this repository?

The entire dataset lives in a single file:

- [`game_list.json`](game_list.json) — a JSON array of objects, one per app or game.

## JSON schema

Each entry in `game_list.json` is an object with the following fields.

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `_comment` | string | **Yes** | Contributor attribution. Use the actual contributor name. For LLM contributions, use the model name (e.g., `Kimi K2.7 Code`), not the harness/interface name. If the data is derived from third-party sources, include the source and license: `contributed by <Name> with attribution as follows: <source> (<URL>, <license>)`. |
| `name` | string | Yes | The international name of the app or game. Preferred be cleaned up to remove SEO strings (eg. "StarterSeeds" instead of "StarterSeeds - Game Launcher") |
| `appStoreID` | integer | Yes | The numeric App Store ID of the app. |
| `bundleID` | string | Yes | The iOS bundle identifier, e.g. `com.example.app`. |
| `igdbID` | integer | No | The IGDB game ID, if one exists. |
| `uriScheme` | string | Yes | The URI scheme used to launch the app, e.g. `exampleapp://`. |

## Required key order

To keep diffs clean and reviews simple, every object must use the following exact key order:

1. `_comment`
2. `name`
3. `appStoreID`
4. `bundleID`
5. `igdbID` (omit if not available)
6. `uriScheme`

### Example entry

```json
{
  "_comment": "contributed by Your Name",
  "name": "Example Game",
  "appStoreID": 123456789,
  "bundleID": "com.example.game",
  "igdbID": 98765,
  "uriScheme": "examplegame://"
}
```

If `igdbID` is not available, the entry should look like this:

```json
{
  "_comment": "contributed by Your Name",
  "name": "Example App",
  "appStoreID": 987654321,
  "bundleID": "com.example.app",
  "uriScheme": "exampleapp://"
}
```

When a contribution is made by an LLM or adapts data from third-party sources, include the source attribution in `_comment`:

```json
{
  "_comment": "contributed by Kimi K2.7 Code with attribution as follows: URI scheme documented by pietropizzi/app-talk (https://github.com/pietropizzi/app-talk, MIT); app metadata from Apple iTunes API",
  "name": "Example Game",
  "appStoreID": 123456789,
  "bundleID": "com.example.game",
  "uriScheme": "examplegame://"
}
```

## Formatting rules

- The root of `game_list.json` is a JSON array (`[]`).
- Use **2 spaces** for indentation.
- Do **not** include trailing commas.
- Keep the file valid JSON. You can verify it with any JSON linter.

## Sorting rule

Currently none in place. Add to the bottom or group related ones together if you like.

## Verification tips

- **App Store ID**: Find it in the App Store URL, e.g. `https://apps.apple.com/app/id479516143` → `479516143`.
- **Bundle ID**: You can extract it from the App Store page source, from tools like [Apple's Enterprise docs](https://developer.apple.com/library/archive/qa/qa1633/_index.html), or by inspecting a purchased app's metadata.
- **URI scheme**: Test it on a real iOS device by entering it in Safari, a shortcut, or the Notes app and tapping the link. Only submit schemes you have confirmed to work.
- **IGDB ID**: Search for the game on [IGDB](https://www.igdb.com) and copy the numeric ID from the URL.

## Attribution

- **Human contributors:** use your name or handle in `_comment` (e.g., `contributed by Your Name`).
- **LLM contributors:** use the actual model name, not the harness or interface name. For example, use `Kimi K2.7 Code`, not `OpenCode`.
- **Third-party data:** if you source a URI scheme or other data from another repository or database, include the source name, URL, and license in `_comment` so downstream users can comply with the original license. For example: `contributed by Kimi K2.7 Code with attribution as follows: URI scheme documented by pietropizzi/app-talk (https://github.com/pietropizzi/app-talk, MIT); app metadata from Apple iTunes API`.
- App Store metadata (`appStoreID`, `bundleID`) is factual data sourced from the Apple iTunes API. IGDB IDs are factual data sourced from IGDB.com.

## License

This project is licensed under the [Creative Commons Attribution 4.0 International License](LICENSE) (CC-BY-4.0).

You are free to share and adapt this data for any purpose, including commercially, as long as you provide appropriate credit and indicate if changes were made.
