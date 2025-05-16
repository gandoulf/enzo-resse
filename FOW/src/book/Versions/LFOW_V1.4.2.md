# LFOW V1.4.2

This version is temporary and minimal as it contains an unfinished feature for "Navigation" and only a few fixes.

## **Feature**

- `Navigation`: AI can now use NavFilters that query the fog state. It's now possible to prevent an AI from moving through the fog.  
  In its current state, this navigation feature does not work with the `CrowdManager`. The feature is not completed yet.

## **Optimization**

- `GPU`: The post-process now computes only the fog state of the team being rendered.

## **Fixes**

- `Collision`: Box collisions can now be attached to a bone. Rotation of the collision was not handled correctly.
- `Entities`: Entities didn't disable themselves properly-crash fixed.
- `Entities`: Fixed shared entity drawer when using `MultiFloor`. Entities were not being drawn anymore and were breaking memory usage.
- `Material`: Fixed compilation for `SM5 (DirectX11)`.
- `Networking`: `FogStateReplication` now allows the client to request a team change -> `ServerRPC_RequestTeamChange(int32)`.

## **Documentation**

- `Navigation`: Added documentation for enabling navigation through fog.
- `Material Opacity`: Updated to warn about performance costs and recommend using `SubFogTexture`.

## **Next Features to Come**

- `Navigation`: AI will be able to use the `CrowdManager`.
- `Android Compilation`: Working on making the plugin available for Android.
- `Teams`: The fog will support up to 32 teams.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_