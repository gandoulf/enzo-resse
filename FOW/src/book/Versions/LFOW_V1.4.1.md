# LFOW V1.4.1

Many fixes + GPU optimization when multiple teams are rendered.

## **Retake**

- `Tiles`: The static variable has been removed and replaced with a shared struct held by the `FOWHandler`. Many symbol errors appeared
during compilation when trying to create custom tiles in another module outside of `FogOfWar`.

## **Optimization**

- `GPU`: The post-process will now compute only the fog state of the team being rendered.

## **Fixes**

- `Console Var`: Commands now properly affect `FOWHandler` in every world.
- `Entities`: Settings are now public be careful with runtime modifications.
- `GPU`: Fixed crash for dedicated servers trying to access GPU memory.
- `Networking`: Fixed a crash in the editor when replication is enabled.
- `Networking`: Client list of teams is now correctly initialized.
- `Rendering`: Fixed GPU fog fragment being too small when the camera is too tilted.
- `Rendering`: `SubFogTexture` was displaying its debug view in the client.
- `Rendering`: Fixed `MPC` initialization for clients in the editor, teams should now display correctly.
- `Stealth Area`: Entering or exiting a stealth area could leave it discovered.
- `Stealth Area`: Fog could blink while entering a stealth area, fixed intersection issues between circles and geometry.
- `Tiles`: `Tiles Heat LUT` static variable has been removed to fix symbol issues when creating `Tiles` classes outside the plugin module.

## **Documentation**

- `Network`: Adding the network diagram
- `Visibility Entity`: Add replication warning regarding Scene Components

## **Next Features to Come**

- `Navigation`: The fog state will affect AI pathfinding.
- `Teams`: The fog will handle 32 teams.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_