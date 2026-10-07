<div align="center">
  <img src="https://i.imgur.com/xi5eEzM.jpeg" alt="Notcha logo" width="220" />
  <h1>Notcha</h1>
  <p><strong>Your everyday tools, right in your Mac’s notch.</strong></p>
  <p>A native macOS workspace for files, notes, music, planning and private AI.</p>
  <p><a href="#install">Install</a> · <a href="#features">Features</a> · <a href="#notcha-ai">Private AI</a> · <a href="#requirements">Requirements</a> · <a href="#build-from-source">Build from source</a></p>
</div>

## A workspace within reach

Notcha turns the area around your Mac’s notch into a compact workspace. Hover or click to open it, get something done, and let it close when you move away. Pin it open when you need more time.

Keep files ready to share, find something you copied, jot down a note, check your next appointment or control your music without opening another window. On displays without a notch, Notcha appears as a floating bar at the top of the screen.

Choose the sections you want and whether Notcha appears in the Dock at first launch. Hide, restore and reorder sections later in Settings. The navigation bar keeps icons centered and switches to smaller controls when more sections need to fit.

**Native SwiftUI and AppKit · No account required · No telemetry · Local AI**


## Notcha AI

Notcha AI uses Apple’s **Foundation Models** framework to process the text you provide on your Mac. Responses stream into the chat, and the session keeps conversational context.

- Rewrite text, summarize it or extract key information and actions.
- Start a new chat or stop a response in progress.
- No ChatGPT account, API key, Ollama installation or remote AI endpoint required.
- Chat content stays in memory while Notcha is open; it is not saved to disk by Notcha.

**Requires macOS 26 or later and a Mac compatible with Apple Intelligence, with Apple Intelligence enabled and the system model downloaded and available.** If these requirements are not met, the chat explains why it is unavailable. Other sections do not require the AI model.

The model works with text you supply. It does not browse the web or automatically read your other apps or clipboard. Results depend on the capabilities of Apple’s model.

## Install

Notcha’s distribution format is a **DMG**, provided through this repository’s **Releases** page. If no DMG is attached to a release yet, use the build instructions below.

1. Download the DMG attached to the release you want to install.
2. Open the disk image and copy **Notcha.app** to **Applications**.
3. Eject the disk image and launch Notcha from Applications.
4. Choose your sections and Dock visibility in the first-launch setup. The Dock icon is enabled by default. Use the menu bar icon to reopen Notcha or access Settings.

### Signing and first launch

The current build uses a local **ad hoc signature**. It is **not signed with Developer ID** and **has not been notarized by Apple**. A DMG or a GitHub release does not change that status.

macOS may block the first launch because it cannot verify the developer or notarization. If you trust the source of your download and choose to proceed, after attempting to open the app, go to **System Settings → Privacy & Security** and use **Open Anyway**, if available, then confirm the prompt.

You do not need to disable Gatekeeper system-wide. See [Apple’s guidance on opening apps safely](https://support.apple.com/102445).

## Requirements

| Item | Current status |
| --- | --- |
| Minimum macOS target | macOS 14 |
| Build architectures | Universal: Apple Silicon (`arm64`) and Intel (`x86_64`) |
| macOS 14 / macOS 15 / Intel hardware | **Not tested**; successful compilation does not establish runtime compatibility |
| Notcha AI | macOS 26+, compatible Apple Intelligence hardware, enabled intelligence and an available downloaded model |
| Interface languages | **English and Italian**, selected in Settings → General → Language. |
| Dock behavior | **Visible by default.** Choose during first-launch setup or change **Show in Dock** in Settings → General. |

Debug and Release universal builds have passed, along with **42 automated tests**. Manual testing has been completed on the developer’s Mac; it does not cover macOS 14/15 or Intel hardware.

## Language

Notcha includes English and Italian translations in the same app. Open **Settings → General → Language**, choose **English**, **Italiano** or **System language**, then quit and reopen Notcha to apply the choice. The setting affects Notcha only. With System language selected, Notcha follows your macOS language preferences.

UI text, menus, permission descriptions, AI suggestions, weather conditions and date labels are localized. Your notes, clipboard contents and saved section identifiers are not translated or modified.

**About Notcha**, available from the menu bar icon and the application menu, shows “Powered by Mxrco”, the app version and [mxrco.dev](https://mxrco.dev).

## Privacy and permissions

Notcha does not add analytics, user accounts or its own backend.

- **Clipboard and file shelf:** kept in memory and cleared when Notcha exits. The shelf stores references to your files rather than duplicating them.
- **Quick notes:** saved locally in `~/Library/Application Support/Notcha/workspace.json`. Notes are not separately encrypted by Notcha.
- **Preferences:** saved locally using UserDefaults.
- **Camera:** local preview only, with no recording or audio capture. The camera stops when its section closes.
- **Calendar, Reminders and music controls:** request the relevant macOS permissions when you use those features. Denied permissions are handled in the interface.
- **Private AI:** text is processed by Apple’s on-device model, with no remote AI requests made by this feature.
- **Weather:** uses an external service, as described below.
- **Lyrics:** when requested, Notcha sends the track title and artist to LRCLIB to retrieve lyrics. Album artwork may also be downloaded from the player’s artwork URL.
- **AirDrop and Shortcuts:** use Apple’s system services. Shortcuts you run can perform their own network requests or other actions.

Clipboard filtering respects sensitive-content markers supplied by source apps. It cannot identify every password or sensitive item that lacks those markers.

### Weather data and external requests

Opening Weather sends the chosen city to **Open-Meteo’s geocoding service**, then sends that city’s coordinates to its forecast service. Notcha does not request your Mac’s location. The initial city is Rome; your chosen city is saved locally.

Open-Meteo receives your IP address and may keep technical logs containing coordinates for up to 90 days, according to its [privacy policy](https://open-meteo.com/en/terms). Notes, clipboard contents and AI messages are not sent to the weather service. The same disclosure is available in **Settings → General → Weather · Privacy and sources**.

Weather data is provided by [Open-Meteo](https://open-meteo.com/), and city data by [GeoNames](https://www.geonames.org/), under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). See [third-party notices](THIRD_PARTY_NOTICES.md) for attribution and display transformations.

The current free API endpoints are intended for **non-commercial use**. Publishing the project on GitHub does not itself authorize commercial API use. Commercial distributions must comply with [Open-Meteo’s service terms](https://open-meteo.com/en/terms).
## Feedback

Use this repository’s **Issues** page to report bugs or suggest improvements. Include your Notcha version, macOS version, Mac model and steps to reproduce the issue. Reports from macOS 14/15 and Intel Macs are especially useful because those configurations have not been tested.

Avoid including personal data, clipboard contents or private chat messages in reports.
