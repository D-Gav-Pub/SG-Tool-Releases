# SG Tool

Desktop companion for law-enforcement workflows: duty automation, loadouts/uniforms, RP command timing, paperwork drafting, hotkeys, and admin/user profile management.

## Features (current)
- **Auth & profiles:** Firebase auth, user roles, badge/callsign/rank storage, and officer ID card rendering.
- **Duty automation:** Clock on/off/change flows that send RP commands (unit creation/disband/rename), uniform and loadout selection, and join/leave unit flows with configurable delays.
- **Loadouts & uniforms:** Manage uniforms, weapons, and loadout presets filtered by allowed roles; select them from the Duty panel.
- **RP timing & strings:** Configure RP delays (text/transition/keystroke/start) and RP lines for clock on/off and role-specific change messaging.
- **Hotkeys:** Configure and persist global hotkeys (desktop).
- **Paperwork assistant:** Draft and save arrest and warrant reports (stored locally via shared_preferences) and generate forum-ready BBCode.
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
> Nothing to note currently
