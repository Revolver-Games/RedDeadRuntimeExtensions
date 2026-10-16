# Third-party components

| Component | Pinned version / commit | License | Included material |
|---|---|---|---|
| [MinHook](https://github.com/TsudaKageyu/minhook) | v1.3.4 / `c3fcafdc10146beb5919319d0683e44e3c30d537` | BSD 2-Clause, plus bundled decoder notices | Source, headers, CMake files, full license |
| [nlohmann/json](https://github.com/nlohmann/json) | v3.12.0 / `55f93686c01528224f448c19128836e7df245f72` | MIT | Single header and full license |
| [Dear ImGui](https://github.com/ocornut/imgui) | v1.91.9b / `f5befd2d29e66809cd1110a152e375a7f1981f06` | MIT; see embedded stb notices | Core, Win32/DX11 backends, headers, license |
| [Vulkan-Headers](https://github.com/KhronosGroup/Vulkan-Headers/tree/v1.2.162) | v1.2.162 | Apache 2.0 | Unmodified core/platform API headers and full license; no Vulkan loader/driver redistributed |

Upstream license text remains under `vendor/` and is copied to distribution `licenses/`. Upstream sources have not been rewritten. The project builds them locally instead of downloading code during configuration.

ScriptHookRDR2 is an optional separately installed runtime provider. No ScriptHook binary, SDK library or source is redistributed. Export spellings were inspected from the user's installed DLL; function prototypes follow its public developer interface.

The alloc8or native database and Cfx/RedM source were consulted as public technical references. Neither database nor Cfx source is bundled or copied. Native identifiers and interface observations are individually documented. Do not assume a permissive redistribution license for an entire database simply because it is publicly readable.

No Rockstar executables, assets, archives, proprietary SDKs, disassembly dumps, decompiled game source or leaked source are included. Exact-build profiles contain short independently located matching signatures and metadata used to validate hooks. RDRX is not affiliated with Rockstar Games.
