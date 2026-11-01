# The Escapists — browser build

The original Fusion events were translated to C++ with Chowdren and compiled to WebAssembly with Emscripten 3.1.74. Rendering uses WebGL. This build runs entirely in the browser and includes its own game assets; the Steam installation is not required.

Use the game’s normal sleep/save behavior. Files persist in IndexedDB for this browser and website origin, including prison map arrays, save slots, settings and unlocks. Writes are queued when files close and flushed when the page is hidden. Clearing site data removes saves; other browsers and domains have separate saves. This is local browser storage, not cloud sync.

For local use, run `python -m http.server 8765` in this directory and open http://127.0.0.1:8765/. Do not open index.html as a file.

The runtime is based on [Chowdren / Anaconda](https://github.com/gfktrin/AnacondaDecompiler), originally by Mathias Kaerlev. Runtime and generated program source are included in `source.zip`, with the GPL v3 text in `COPYING.txt`. Third-party components retain their notices in the source archive. The game’s original art, music and other assets remain under their respective rights; the runtime license does not grant rights to those assets.

To rebuild: extract source.zip, activate Emscripten 3.1.74, and run `emcmake cmake -S source -B build -G Ninja`, then `cmake --build build --parallel 4`. Output is in build/web. The build uses Emscripten SDL2, zlib and OpenAL ports. All custom browser runtime, storage, renderer and path compatibility changes are in the archive.

This is a compatibility port, with menus, tutorial movement/inventory and save/load checked. It has not received a complete prison-by-prison playthrough. Steam integration is stubbed; some runtime features may still differ from the Windows version.
