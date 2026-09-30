# Changelog

All notable user-facing changes to AVDKit are documented here. This is the public
distribution changelog; it focuses on features and behavior, not implementation.

---

## 2.0.0 — Workspace redesign

A ground-up redesign of AVDKit around a sidebar workspace, a command palette,
dark/light themes, a rebuilt device console, and a full Frida workbench.

### New workspace shell
- Redesigned main window as a sidebar workspace with four pages: **Overview**, **Virtual Devices**, **Connected Devices**, and **Tools**.
- **Overview**: status cards (AVDs, running emulators, connected devices, SDK components), an environment card with one-click installs for missing components, and a quick-launch card.
- **Virtual Devices**: searchable AVD list with details panel and saved launch options; stop running emulators and launch several at once.
- **Connected Devices**: live device table with per-device HTTP proxy and shortcuts to device tools.
- **Tools**: filterable launcher grouped as Security testing, Device utilities, and Network & certificates.
- **Command palette** (`Ctrl+K`): fuzzy search across pages, tools, AVDs, devices, and actions.
- **Console**: color-coded, filterable activity output with copy/export/clear and an unread-error badge (toggle with `` Ctrl+` ``).
- New shortcuts: `Ctrl+1…4` to switch pages, `Ctrl+R` launch, `Ctrl+N` create, `Ctrl+E` edit, `F5` refresh, `F1` manual, `Ctrl+Q` exit.

### Theming
- Dark, light, and match-system themes with four accent colors, applied across every window.
- New **Appearance** preferences page with live preview (Cancel reverts); appearance changes no longer require a restart.

### ADB Device Manager (rebuilt)
- Rebuilt into a tabbed console: **Overview · Apps · Files · Screen · Shell · Network**, with a shared device selector and a command log.
- **Overview**: richer device dashboard (model, Android/API, ABI, brand, serial, root, storage, battery, resolution, density, Wi-Fi IP, uptime) plus quick controls (keyevents, send text, rotate, Wi-Fi/data toggles, reboot menu).
- **Apps**: app manager with a searchable package list and per-app actions — launch, force-stop, clear data, App Info, extract APK, permissions, enable/disable, uninstall, plus APK / split-APK install.
- **Screen**: scrcpy screen mirroring and control, one-click screenshot, and screen recording.
- **Shell**: run arbitrary `adb shell` commands with scrolling output, alongside logcat capture.
- **Network**: HTTP proxy set/clear plus a port-forwarding manager (forward/reverse list, add, remove).
- **Files**: device file explorer with a new "New Folder" action alongside upload/download/delete and push/pull.

### Frida Workbench
- The Frida Utility is now a full security-testing workbench, replacing the separate **Runtime Hook Launcher** and **TLS & Pinning Analyzer** (both removed).
- Spawn a package or attach to a running app.
- Curated preset library (SSL/TLS pinning bypass, root-detection bypass, crypto/digest logger, WebView inspection, clipboard/intent logger, native tracer), plus local files and CodeShare downloads — combinable and editable in-app.
- `frida-trace` mode for native and Java patterns.
- Root-aware frida-server management: downloads the matching server and starts it with the correct privileges, reporting which user it runs as.

### Certificates & network
- Retired the standalone **Traffic Interceptor**. Setting a device HTTP proxy now lives on the Connected Devices page, and installing a CA lives in the System Certificate Manager.
- **System Certificate Manager** hardened: installs run in the background with progress and per-step logs, use a persistent system-trust install with an automatic dm-verity fallback, and now appear under **Settings → Trusted credentials → System** and survive reboots.

### App Backup & Restore
- The single-APK extractor is now a bulk **App Backup & Restore** tool.
- **Backup**: multi-select apps, always capturing APK + split APKs, optionally external data + OBB and — with root — internal app data. Each app is saved to its own folder with metadata.
- **Restore**: scan a backup folder and reinstall selected apps, optionally restoring data/OBB (and internal data with root).

### Responsiveness & reliability
- Device polling, proxy commands, update checks, and diagnostics no longer block the UI.
- Several emulators can be launched and tracked at once; closing AVDKit offers to stop the ones it launched.
- Mouse-wheel scrolling no longer changes combo boxes or spin boxes unless focused.
- Fixed crashes when starting SDK commands while an emulator was running, retry loops on failed installs during setup, and window-close no longer leaving the process running.

---

## 1.1.0 — Feature & UX expansion

### Highlights
- Added the **APKTools** workflow (decompile, build, zipalign, sign) with integrated tool download.
- Added a tabbed **Frida Setup + Execution/Hooking** workflow with improved setup automation and runtime controls.
- Improved **Create AVD** with installed-image management (download/delete state handling).
- Enhanced quick ADB controls and direct entry points for common actions.

### Frida improvements
- Split the Frida workflow into **Frida Setup** and **Frida Execution / Hooking**.
- Added frida-server lifecycle controls (refresh status, start, stop) with running-state and permission visibility.
- Added device package fetch, an editable package dropdown, and type-ahead matching.
- CodeShare downloads now persist between sessions.

### APKTools (new)
- Automatic APKTool download and version selection.
- Decompile, build, zipalign, and debug-sign operations with inline progress and path helpers.

### AVD creation & image management
- Added delete-installed-image support in Create AVD.
- Download/Delete button now reflects the selected image's install state, with a safe confirmation flow.

### ADB Device Manager / Explorer
- Added an **Upload** control (file or folder) targeting the current explorer directory.
- Added preferred-device selection when opening the manager from quick controls.

### Main window
- Added a `+` shortcut to open Create AVD directly, a compact icon-only refresh, and an icon-only Manage ADB Devices shortcut.
- Aligned release/update and issue-reporting links.

### Platform support
- ✅ Windows installer · ⏳ Linux (planned) · ⏳ macOS (planned)

---

## 1.0.0 — Initial release

### Highlights
- First stable baseline of AVDKit with core emulator and device functionality.
- Application structure and build pipeline established.
- Basic documentation and usage guidelines added.

### Build & distribution
- Windows installer (`.exe`) published via the distribution repository.
- Installer does not require administrator privileges.

### Platform support
- ✅ Windows installer · ⏳ Linux (planned) · ⏳ macOS (planned)
