# SG Tool

Desktop companion for law-enforcement workflows: duty automation, loadouts/uniforms, RP command timing, paperwork drafting, hotkeys, and admin/user profile management.

## Features (current)
- **Auth & profiles:** Firebase auth, user roles, badge/callsign/rank storage, and officer ID card rendering.
- **Duty automation:** Clock on/off/change flows that send RP commands (unit creation/disband/rename), uniform and loadout selection, and join/leave unit flows with configurable delays.
- **Loadouts & uniforms:** Manage uniforms, weapons, and loadout presets filtered by allowed roles; select them from the Duty panel.
- **RP timing & strings:** Configure RP delays (text/transition/keystroke/start) and RP lines for clock on/off and role-specific change messaging.
- **Hotkeys:** Configure and persist global hotkeys (desktop).
- **Paperwork assistant:** Draft and save arrest, warrant, and traffic stop reports (stored locally via shared_preferences) and generate forum-ready BBCode.
- **Heli tools:** Tail numbers, landing sites, and checklist settings.
- **Admin:** Role management for users (admin-only section).
- **About & updates:** Shows current version/build and checks the public releases feed (`D-Gav-Pub/SG-Tool-Releases`) for updates; links to the latest download.

## Install (Windows MSIX)
1) Trust the publisher cert (first-time only):
   - Double-click `DGav.cer` (shipped with the release), choose **Current User** (or **Local Machine** for all users), and install it into **Trusted Root Certification Authorities**.
   - Repeat for the same `DGav.cer`, installing into **Trusted People**.
2) Run `sg_tool.msix` from the release. Publisher should show `DGav`; install will proceed without trust errors.
3) Updates: install the newer MSIX over the existing app; settings and saved drafts are preserved (`%APPDATA%\\com.dgav.sgtool\\shared_preferences.json`).

## Changelog
### 1.0.1
#### Reports
- Added a GOB Traffic Stop report builder with draft saving and BBCode output.
- Added a Gang Incident report builder with draft saving and BBCode output.
- Added a SEB Operation report builder with draft saving and BBCode output.
- Added draft delete functions so reports without it
- Arrest report: DOC Sign Away shows a custody transfer memorandum preview and auto-sends DOC handover RP lines using saved officer info/timing (with long suspect lists chunked across /do lines).
- Supervisor paperwork: new Weekly Inactivity Notices tool that lets supervisors paste weekly names, enter profile links, and step through warning/log/email BBCode with collapsible live previews and completion checkboxes.
- Templates for warnings/logs/emails are hidden by default with an edit toggle, include the latest mandated wording, and render preview styling (colors, bullets, inline links) for quick visual checks before posting.

#### Fixes
- Changed the Heli Menu Delta Callsigns to be AIRSD-7 and AIRSD-8
- Arrest report: sidebar actions now use a 2x2 grid (Load, Delete, Reset, DOC Sign Away) to keep labels horizontal and tidy.
- Warrant report: sidebar load/delete/reset buttons now use the same 2x2 grid to keep labels horizontal.
- Saved draft dropdowns now ellipsize long titles and load/delete grids wrap responsively across all report/email screens with load functions, preventing vertical label overflow.
- /gate and /paytoll now work as intended

## Release process (maintainers)
- Bump `version:` in `pubspec.yaml`.
- `flutter clean && flutter pub get`
- Build Windows: `flutter build windows --release`
- Sign/package MSIX: `dart run msix:create --release --build-windows=false`
- Verify signature: `Get-AuthenticodeSignature build/windows/x64/runner/Release/sg_tool.msix` -> `Status: Valid`, `CN=DGav`
- If the cert changed, re-export `windows/runner/DGav.cer` and include it in the release
- Publish to `https://github.com/D-Gav-Pub/SG-Tool-Releases` with tag `vX.Y.Z` and attach:
  - `sg_tool.msix`
  - `DGav.cer` (if updated)
  - (Optional) ZIP of `build/windows/x64/runner/Release/`

## Notes on data retention
- Saved drafts and preferences live in the platform app-data directory (Windows: `%APPDATA%\\com.dgav.sgtool\\shared_preferences.json`); MSIX upgrades keep this intact.
- Avoid uninstalling with "remove app data" if you need to preserve settings.
