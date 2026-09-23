# LFOW V1.6.1

This update focuses on networking robustness (seamless travel, dedicated servers) and adds new terrain-oriented tools.

## **Features**

- `Collision`: Added `AFOW_CollisionE_Terrain`, an editor generator that fills FOW collision under a `Landscape`
  automatically, following the terrain's actual silhouette.
- `Debug`: Added a `Fog Of War Colliders` show flag to visualize collider and stealth area volumes in editor.
- `Handler`: Added Blueprint/C++ setters (`SetFOWRenderEnabled`, `SetChannelMask`, etc.) to control FOW render
  settings at runtime, including in Shipping builds where console commands are disabled.

## **Optimization**

- `Collision`: Shadow geometry computation is now faster (10ms → 8.5ms for 1000 entities).
- `Debug`: Fixed the collider/floor editor visualizers rendering (and costing render thread time) during PIE.

## **Fixes**

- `Networking`: Fixed seamless travel setup, including a potential crash in `PlayerCameraManager`.
- `Networking`: Fixed shared layers in a `Floor` sending the wrong drawer update to tiles.
- `Networking`: Fixed several dedicated server issues.
- `Networking`: Fixed `FogTextureAssets` when using PIE multiplayer.
- `Rendering`: Fixed the stylized fog material.

## **Documentation**

- `Entities`: Added documentation for `AFOW_CollisionE_Terrain`, including FOWHandler-limited generation and the collider display show flag.
- `Networking`: Added a note about `Seamless Travel`

## **Next Features to Come**

- `Rendering`: Terrain fog card material.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_