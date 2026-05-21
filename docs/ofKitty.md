# ofKitty

*openFrameworks with Edit mode. Pi-native. Web-native.*

ofKitty is an openFrameworks **advocacy and addon ecosystem** built around **composition over inheritance**, **always-on Edit mode**, and targets that stay small enough to matter on real hardware.

**Start from stock OF.** Use [openframeworks/openFrameworks](https://github.com/openframeworks/openFrameworks) and add only the addons you need. The toolkit stays `ofApp`, `ofMain.h`, and the addon model you already know — not a rewrite.

[ofKitty/openFrameworks](https://github.com/ofKitty/openFrameworks) is for development convenience — and should not br a requirement, just an excuse to patch `libs/openFrameworks` and speed.

---

## Pillars

### 1. Do not fork the core — extend with addons

openFrameworks is already open. We believe **everything we need can live in addons**, scripts, and kit layers — not in patches to `libs/openFrameworks`. Keep it light!

- Prefer `ofxKit`, `ofxEnTTKit`, and companion **Kit** addons over core changes.  

### 2. Keep OF small and portable

The base distribution should stay **lean**. Features, editors, machine UIs, and domain tools ship as optional addons.

- **Core spine** — ECS runtime, inspector, ImGui integration (`ofxKit` and friends).
- **Everything else** — plotters, GRBL, audio kits, etc. — opt-in addons you add to `addons.make`.

Smaller surface area means faster builds, easier updates, and fewer surprises when you move between targets.

### 3. Design for the smallest device you actually ship

**Raspberry Pi is our minimum bar.** If it runs well on a Pi, the architecture is honest. Desktop conveniences are welcome; Pi constraints are non-negotiable here.  

- Pi-first defaults: sensible memory use, build paths that work on ARM Linux, MSYS2/embedded workflows where we maintain them.
- Desktop-only sugar belongs in addons, not in assumptions every sketch must pay for.

### 4. Composition-first creative coding

Sketches stay close to standard OF. Edit mode, inspectors, and ECS registries attach through **`ofkitty::Runtime::attach()`** in `main.cpp` — see [ofxKit](https://github.com/ofKitty/ofxKit) for usage and API.

### 5. Web-native and always-on Edit mode

Targets include **Emscripten / web** and runtimes where **Edit mode** (Cmd-E / Ctrl-E) is a first-class overlay, not a separate “tools build.”

---

## Platforms

| Platform | Role |
|----------|------|
| **Raspberry Pi (Linux ARM)** | **Minimum supported target** — primary reference device. |
| Desktop (Windows, macOS, Linux) | Development and authoring. |
| **Web (Emscripten)** | Shipping and sharing sketches in the browser. |
| **Embedded** | **Roadmap** — we want OF-class creative coding on the smallest useful hardware; expect dedicated addons and constrained profiles, not a fat default distro. |

> ESP export is aspirational today: APIs and build plumbing will land in addons, without pulling the full desktop into firmware images.

---

## Repositories

| Repo | Purpose |
|------|---------|
| [openFrameworks](https://github.com/ofKitty/openFrameworks) | `ofKitty` branch with spine addons + scripts |
| [ofxKit](https://github.com/ofKitty/ofxKit) | Composition runtime, Edit mode overlay |
| [ofxEnTTKit](https://github.com/ofKitty/ofxEnTTKit) | ECS components & systems for OF types |
| [ofxEnTTInspector](https://github.com/ofKitty/ofxEnTTInspector) | ImGui inspectors for ECS |
| [ofxAbletonLinkKit](https://github.com/ofKitty/ofxAbletonLinkKit) | fxKit bridge for network tempo and sync |
| [ofxGrblKit](https://github.com/ofKitty/ofxGrblKit) | Example kit addon (GRBL / plotter UI) |
| [apothecary](https://github.com/ofKitty/apothecary) | Prebuilt lib formulas & releases |

---

> Contributions are welcome.

---

## See also

- [README.md](README.md)
- [Getting started](getting-started.md)
- [Build speed](build-speed.md) — `make -j xof`, ccache, fast iteration on stock OF
- [ofxKit README](https://github.com/ofKitty/ofxKit/blob/master/README.md) — attach API, shortcuts, architecture
