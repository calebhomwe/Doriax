# Doriax

Snapshot of a local Doriax engine install:

- `doriax-editor.exe`, `doriax-editor-cmd.exe`, `doriax.dll`, `doriax.lib`: prebuilt
  **Windows** editor and engine binaries
- `engine/`: engine source (C++17, CMake) with bundled third-party libs
  (sokol, Jolt, Box2D, Lua/LuaBridge, SoLoud, tinygltf, ...) and a minimal sample
  project in `engine/project/`
- `settings.yaml`, `editor_layout.ini`: the editor's local settings

## Play / Test

On Windows, run `doriax-editor.exe`.

On Linux, the engine and the sample project compile and link from source
(verified on Ubuntu 24.04 with GCC):

```bash
sudo apt-get install -y build-essential cmake libgl-dev libx11-dev libxi-dev libxcursor-dev libglfw3-dev
cmake -S engine -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j"$(nproc)"      # -> build/libdoriax.a + build/doriax-project
```

The sample binary starts, but it then stops with "missing precompiled shaders"
(`assets/shaders`). Shaders are compiled by the editor
(`doriax-editor shaders --out assets/shaders --platform linux ...`), which ships
here only as a Windows build. CI (`.github/workflows/build.yml`) runs the Linux
compile on every push and PR.
