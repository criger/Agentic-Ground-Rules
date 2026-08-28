# Mixed Reality (HoloLens and UWP)

Mixed reality apps on HoloLens add a holographic rendering pipeline, spatial
coordinate systems, device-capability gating and UWP packaging constraints that
differ from a standard desktop or web application. The same responsibility
boundaries apply, but the framework vocabulary changes.

## Architecture vocabulary

| Architectural role | HoloLens / UWP example |
| --- | --- |
| View | `HolographicSpace`, `HolographicFrame`, holographic camera render targets |
| Controller / coordinator | `HolographicAppMain` or `AppMain` — frame loop orchestrator |
| Model | domain objects (e.g. `Satellite`, `TleRecord`) and sealed-state types |
| Service / use case | `OrbitService`, `GeolocationService`, business-rule services |
| Repository / client | data-source wrappers for remote API (e.g. CelesTrak) and local config |
| Integration / mapper | `HttpClient` clients, TLE parsers, coordinate system mappers |
| Config | centralized constants (e.g. dome radius, ceiling offset), app manifest capabilities |

## MR-specific rules

- Keep the holographic render loop focused on present/update cycles. Do not
  place business logic, network calls or heavy computation inside `Render()` or
  `Update()` without explicit off-threading.
- Use `HolographicFramePrediction` every frame for head pose and camera poses.
  Always read `SpatialPointerPose` from the prediction timestamp, not from the
  current device time, to avoid input lag.
- Separate world-locked content from head-locked content clearly. World-locked
  holograms require `SpatialStationaryFrameOfReference` or `SpatialAnchor`;
  head-locked UI (e.g. debug panels) follows the camera directly.
- Gate every new API call behind `ApiInformation.Is*Present()` when targeting a
  min-version lower than the API's introduction version. HoloLens 1 (build
  10240) and HoloLens 2 (build 19041+) expose different surfaces; do not
  assume an API exists at runtime.
- Treat the UWP min/target platform version as a contract. A change to
  `TargetPlatformMinVersion` or `TargetPlatformVersion` in the `.csproj`
  affects the installed base and may break older devices. Do not bump it
  casually.
- Keep a single authoritative `HttpClient` (or equivalent) and document its
  timeout and endpoint list. Do not instantiate per-call clients; UWP
  connection pooling is per-app and losing it causes socket exhaustion.
- Prefer fallback data for time-critical services (e.g. hardcoded TLEs when
  CelesTrak is unreachable). A holographic app that shows nothing for 30
  seconds while retrying a network call is a poor experience.
- Keep user-visible strings and labels in a central source, not inline.
  Accessibility labels are content, not styling.
- Preserve the app's privacy and capability posture. UWP `Package.appxmanifest`
  capabilities (location, webcam, microphone) must match actual usage; unused
  capabilities are a Store rejection risk and a trust signal to the user.
- Do not mix SharpDX 3.x and 4.x in the same project. SharpDX 3.0.2 is the
  only version that compiles under .NET Native (x86 AOT) for HoloLens 1.
  Upgrading to 4.x breaks the release build silently at link time.
- Render to each camera in `prediction.CameraPoses` every frame. The holographic
  pipeline is stereoscopic by default; skipping a camera produces one-eye
  content and breaks depth perception.

## UWP build and CI constraints

- `dotnet build` cannot resolve Windows XAML/UWP targets. Use MSBuild from
  Visual Studio 2022 on a `windows-2022` runner. Newer runner images
  (e.g. `windows-2025`) are incompatible with the legacy UWP/HoloLens 1 SDK.
- Release builds for HoloLens 1 must target `x86` with
  `UseDotNetNativeToolchain=true`. Debug builds may use x64 for faster
  iteration, but the Store submission path is x86 only.
- Keep the Windows SDK version pinned to the minimum that supports the target
  device. For HoloLens 1, that is `10.0.19041.0`.
- WACK (Windows App Certification Kit) validation must pass before Store
  submission. Include it in the CI pipeline for tagged releases.
- Store submission requires Partner Center credentials (`AZURE_AD_TENANT_ID`,
  `AZURE_AD_CLIENT_ID`, `AZURE_AD_CLIENT_SECRET`, `SELLER_ID`) configured as
  repo secrets. Never hard-code them.

## Spatial coordinate systems

- `SpatialLocator.GetDefault()` gives the device's world-tracking origin.
- `CreateStationaryFrameOfReferenceAtCurrentLocation()` is the simplest way to
  get a world-locked coordinate system at app launch. It may drift slightly as
  the system learns the environment.
- `SpatialAnchor` provides drift-free positioning for content the user marks as
  important. Anchors can be saved to `SpatialAnchorStore` for session
  persistence.
- Always transform coordinates through the correct `CoordinateSystem` when
  combining data from different sources (e.g. GPS-derived positions with
  holographic render targets).

## Performance constraints

- Target 60 fps consistently. Dropped frames are immediately noticeable in
  mixed reality and cause discomfort.
- Batch constant buffer updates per-frame rather than per-object when possible.
  A single `UpdateSubresource` call for a model matrix buffer is cheaper than
  one per hologram.
- Use VPRT (Vertex Position and Render Target Index) shaders when the device
  supports them to avoid geometry shader overhead for instanced stereo rendering.
  Fall back to geometry shaders on older hardware.
- Keep the DOM-equivalent (HTML/UI overlays) out of the holographic render path.
  Use `HolographicSpace` and Direct3D only for holograms; use XAML `Popup` or
  `SwapChainPanel` only when a UWP UI element is genuinely needed.

## Existing systems

Do not reorganize a working holographic app as part of an unrelated fix.

1. Understand the existing holographic pipeline and frame loop.
2. Place new content in the clearest available layer (renderer, service, model).
3. Preserve existing coordinate system conventions and billboard behavior.
4. Preserve public behaviour and contracts.
5. Propose broad restructuring separately when it needs wider validation.

Improve the holographic experience incrementally without turning a small repair
into a risky pipeline rewrite.
