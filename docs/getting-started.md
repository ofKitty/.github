# Getting started

### 1. Install OF

Use [`install_from_github.sh`](scripts/dev/install_from_github.sh) to walk though the steps outlined setup guides.

> This should be an addon. ofxForDummies

### 2. Add Spine (Edit Mode)

Clone into `addons/`:

- `ofxKit`
- `ofxEnTT`
- `ofxEnTTKit`
- `ofxEnTTInspector`, 
- `ofxImGuiStyle`

## 3. Build

In your app folder:

```bash
make -j xof
```

See [Build speed](build-speed.md) for `ReleaseNoOF`, ccache, and platform notes.

### 4. Attach in `main.cpp`

```cpp
#include "ofMain.h"
#include "ofApp.h"

int main() {
    ofGLWindowSettings settings;
    settings.setSize(1024, 768);
    auto window = ofCreateWindow(settings);
    auto app = std::make_shared<ofApp>();
    ofkitty::Runtime::attach(window, app);
    ofRunApp(window, std::move(app));
    ofRunMainLoop();
}
```

Press **Cmd-E** or **Ctrl-E** to toggle Edit mode. Full API: [ofxKit README](https://github.com/ofKitty/ofxKit/blob/master/README.md).

### Next

- [Philosophy](ofKitty.md)
- [Build speed](build-speed.md)
