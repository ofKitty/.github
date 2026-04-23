# openFrameworks speed builds

We all like speedy builds! nobody likes to wait.
No need to compile OF every time.

## Daily command (use this)

```bash
make -j xof
```

> `xof` = exclude OF core rebuild — shorthand for `ReleaseNoOF` 

| Goal | Command |
|------|---------|
| **Iterate app / addons** | `make -j xof` |
| **Debug iteration** | `make -j xdof` |
| **After changing OF core or platform libs** | `make Release -j` |
| **Init clean machine** | `cd $OF_ROOT/libs/openFrameworksCompiled/project && make -j` then app `make -j xof` |

---

## ccache — install per platform

Enable in your app’s **`config.make`** (after installing `ccache`):

```make
USE_CCACHE = 1
```

First build is still full price; later edits to a single `.cpp` are typically seconds.

### Windows (MSYS2)

Use the package that matches **`echo $MSYSTEM`**:

| `MSYSTEM` | Install |
|-----------|---------|
| `UCRT64`  | `pacman -S mingw-w64-ucrt-x86_64-ccache`  |
| `MINGW64` | `pacman -S mingw-w64-x86_64-ccache`       |
| `MINGW32` | `pacman -S mingw-w64-i686-ccache`         |
| `CLANG64` | `pacman -S mingw-w64-clang-x86_64-ccache` |
| `CLANG32` | `pacman -S mingw-w64-clang-i686-ccache`   |

`scripts/ci/msys2/install.sh` in OF installs `$MINGW_PACKAGE_PREFIX-ccache` when you use the CI install path.

### Linux (Debian / Ubuntu / Mint)

```bash
sudo apt install ccache
```

### Linux (Arch)

```bash
sudo pacman -S ccache
```

### Linux (Fedora / RHEL)

```bash
sudo dnf install ccache
```

### macOS

```bash
brew install ccache
```

Optional: `export CC="ccache clang"` / `export CXX="ccache clang++"` in your shell profile, or rely on `USE_CCACHE = 1` in `config.make` for makefile projects.

### Linux ARM / cross-compile (RPi toolchains)

Same distro package on the **host** (`ccache`); point `CC`/`CXX` at `ccache arm-linux-gnueabihf-g++` in your environment or wrapper scripts (see OF `scripts/ci/linuxarmv7l/`).

### Emscripten

Install `ccache` on the host, then use emsdk’s compilers through ccache (OF emscripten CI uses `emmake make`; you can wrap `emcc` similarly). Slower domain than desktop; still helps on large addons.

### Android

Core builds via **Gradle + CMake** in Android Studio, not `ReleaseNoOF`. Use Android Studio’s build cache / NDK; optional host `ccache` for native code is a separate Gradle/NDK setup — not covered by the classic project makefile.

### iOS / tvOS

Xcode builds; host `brew install ccache` and Xcode-specific ccache integration if you maintain custom xcconfigs. Not makefile-driven.

---

## Other habits

1. **Stable `config.make`** — changing `CFLAGS` / includes rewrites `.compiler_flags` and forces a full app+addon rebuild.
2. **Heavy headers** (EnTT, ImGui, etc.) — keep them in `.cpp` files, not umbrella headers, to shrink rebuild graphs.
