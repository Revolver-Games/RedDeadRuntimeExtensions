# RDRX — Red Dead Runtime Extensions

An unofficial Windows x64 native runtime and compiled C++20 module SDK for **offline RDR2 Story Mode**. Plugins use `.SAAS`: **Such An Advanced Script**.

This repository contains a built, tested development foundation. It is **not a finished split-screen implementation or an in-game-certified production release**. No undocumented RDR2 detour is enabled by default. Unverified features return an explicit unavailable result.

## Start here

For the newly integrated private VPS mode, see [online preview setup](docs/online-preview.md) and [Ubuntu server setup](server/README.md). It retains local split-screen and adds a two-player presence preview; shared combat and missions are not implemented.

```powershell
./tools/build.ps1 -Configuration Debug -Configure -Test -Install
./tools/build.ps1 -Configuration Release -Test -Install
```

The script discovers MSVC and the Windows SDK, sets a process-local build environment, and uses Ninja Multi-Config. Sources and pinned open-source dependencies are included; builds require no network access. See [building](docs/building.md).

After building:

```powershell
./build-ninja/bin/Release/rdrx_host.exe --self-test ./build-ninja/examples/Hello/Release/Hello.SAAS
./build-ninja/bin/Release/rdrx_dashboard.exe
./build-ninja/bin/Release/rdrx_discover.exe 'C:/Program Files/Rockstar Games/Red Dead Redemption 2/RDR2.exe' signatures/registry.json reports/discovery.json
```

`dist/` contains `rdrx.asi`, tools, a lifecycle example, configuration, signatures, documentation, compiled SDK libraries, module interfaces and compiler-specific IFC files. Debug and Release SDK libraries live in separate directories; installing Release last makes the top-level runtime/tools the Release binaries.

## What works now

- Versioned C ABI, `.SAAS` manifests, SHA-256 verification before loading, dependencies, capability checks, quiescence guards and cooperative hot unload.
- Module imports (`RDRX`, `RDRX.Events`, `RDRX.World`, `RDRX.Input`, `RDRX.Entities`) backed by `RDRX.Core.lib`.
- Typed event payloads, owner-scoped subscriptions, bounded game-thread jobs, extensible console, structured JSON logs and optional crash diagnostics.
- Bounds-checked PE inspection, module enumeration, wildcard scanning, relative/RIP-relative resolution, protected memory access, fingerprinted signature cache and JSON discovery reports.
- MinHook lifecycle management with original-byte validation, foreign-patch rejection, retained trampolines, dependencies and timing instrumentation.
- Four XInput controller snapshots, Raw Input observation utilities, logical local-player contexts and observed entity references.
- ScriptHookRDR2 bridge for script ticks, Story Mode predicates and reviewed scalar native queries.
- Dear ImGui modular developer panels, headless UI tests and a real Win32/DX11 dashboard backend.
- Experimental local controller routing and a separately controlled Arthur ped. Independent movement was confirmed in Story Mode, and automatic death/respawn was verified with a new ped identity after five playable seconds.
- An experimental Vulkan compositor displays retained John-left and Arthur-right camera pictures with a vertical divider. The user confirmed the two-view output in Story Mode. Cameras alternate, so each view refreshes more slowly; this is not simultaneous world rendering. See [the split experiment](docs/experimental-split.md).

See [local co-op development](docs/local-coop-development.md) for controls, the requested John-left/Arthur-right layout, installation and the precise remaining limitations. Experimental plugins ship separately from default autoload.

## What remains unavailable

Independent script/native engine binding, complete pool generations, deep engine events, complete player behavior for the secondary ped, per-player HUD/targeting/inventory, simultaneous world render passes, and dual streaming interests require further work. The logical context API reserves data ownership and device assignment; it does not make a second ped a second native player. Entity references do not yet prove safety against unobserved same-slot/same-model reuse.

The public native API permits seven scalar read operations. The experimental co-op plugin has a private typed bridge for the reviewed vector, pointer and mutating operations it owns. This does not expose unrestricted invocation through the public ABI.

## Game integration

Read [live integration](docs/live-integration.md) and [runtime testing](docs/runtime-testing.md) before deployment. Use an existing compatible ASI loader and ScriptHookRDR2. RDRX does not replace `dinput8.dll`, `version.dll`, ScriptHookRDR2 or existing mods. During this development session, only the owned `rdrx.asi` and `rdrx.path` files were added to the user's game directory; configuration, logs and test plugins are in a separate writable workspace directory.

The installed executable is **1.0.1491.50**. Script registration, Story Mode ticks and scalar native reads have now run inside the game. Live testing exposed and fixed a 32-bit native return-width bug. Optional pass-through observers require explicit activation and exact executable/prologue verification; they do not provide split-screen. See [live observations](reports/live-observation.json), the [crash investigation](reports/crash-investigation.md), and [live integration](docs/live-integration.md) for the evidence and its limits.

## Development map

Start with [architecture](docs/architecture.md), [plugin system](docs/plugin-system.md), [SDK](docs/sdk.md), [hook matrix](docs/hook-requirements.md), [split-screen architecture](docs/splitscreen-architecture.md), and [implementation status](docs/implementation-status.md). The [baseline validation report](reports/validation.json) and [original implementation review](docs/final-review.md) describe the first foundation build, before live deployment. The [live integration notes](docs/live-integration.md) describe the subsequent work. External research and licensing are recorded in [references](docs/references.md) and [third-party notices](THIRD_PARTY.md).
