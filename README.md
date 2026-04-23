# ofKitty

*openFrameworks with Edit mode. Pi-native. Web-native.*

A collections of addons for [openFrameworks](https://openframeworks.cc/) aimed at **always-on Edit Mode**, **Raspberry Pi**, and the **web**. The addon ecosystem behaves the same as **stock** [openFrameworks](https://openframeworks.cc/). We like fast builds (`make -j xof`), have a strong preference for composition-first systems, however this is not enforced.

This addon structure creates a layered ECS platform:

| **ofApps** |
| :--- |
| `ofxEnTTInspector` (and other ECS addons) |
| **ofxEnTTKit** — components, systems, ofNode bridge |
| **openFrameworks** — GL, window, events, I/O |

> We do **not** fork OF core for features and we love the feel of a fresh `ofApp` sketch.

## Docs

| | |
|---|---|
| [Philosophy](docs/ofKitty.md) | About ofKitty |
| [Getting started](docs/getting-started.md) | Stock OF + spine addons, or optional kitty tree |
| [Build speed](docs/build-speed.md) | `make -j xof`, ccache, platform install notes |

The org profile on [github.com/ofKitty](https://github.com/ofKitty) is [`profile/README.md`](profile/README.md).
