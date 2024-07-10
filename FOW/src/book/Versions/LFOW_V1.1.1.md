# LFOW V1.1.1

Quick fixes after the release of the plugin

**Fixes:**

- `Replication`, The FOW wasn't easy to implement in new projects, and teams weren't correctly replicated in the drawer or entity.
- `Replication`, FogStateReplicationClient is now correctly deleted when a client disconnects.
- `Minimap`, Minimap had the Z value hardcoded to 0 in the material; it now uses the value provided by "MinimapPlanLocation."
- `TextureSample`, Frustum texture sample math wasn't correct for super thick floors. This issue resulted in offset fog in the render.
- `Material`, Fix the material "M_FOW_Visibility_Dithering" present in the feature showcase map, dithering shadow wasn't appearing correctly.

**Documentation:**

- `Networking` documentation has been updated.

**LayeredFOW_Demo:**

- A template map for `Networking` is now provided in this project. You can migrate `TemplateProject` folder to your `UE5.4 project` to set up an online game.

**LFOW compatibility**:

- The plugin for Unreal versions `5.2` and `5.3` doesn't work due to a lack of knowledge on my part. A friend briefed me, and I will make the necessary corrections. As a result, the release of `LFOW V1.1.1` for these two versions will be delayed a bit.

That's all for the quick fixes. Don't hesitate to ping me on my `Discord` if you find issues or if you'd like to submit a feature idea!

**Next features to come:**

- `FogHeatTexture`: Will display a smoother fog transition.
- `Bush system`: Will be designed as MOBA games did.
---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_