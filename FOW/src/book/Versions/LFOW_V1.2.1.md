# LFOW V1.2.1

Adding Linux compatibility, bug fixes, documentation update.

**Features**

- `Linux` is now supported.
- `Stealth Area` Enum is now available: Fog_Shadow / Fog / No_Fog.
- `Team Mask` Drawers with a team set to -1 were updating the fog of each team. A mask is now available to select which team is affected (limited to 32 teams).

**Fixes**

- `HeatTexture`: Fixed HeatTexture merging when the number of bits used is smaller than the TilePixelSize.
- `Entities`: Fixed crash with 1-floor fog setup when entities go out of bounds without being volatile.
- `Stealth Area`: Fixed crash when turning off and on the entity.
- `AABBTree Collision`: Fixed crash during regeneration.
- `Fog Rendering`: 1 channel tiles can now be selected without having to update the Post Process (Using 1 channel for MOBA games improves performance).
- `Fog Rendering`: Fixed 1 and 3 channel tiles update issues when having many teams.
- `Networking`: Fixed network initialization happening in the editor.
- `FOVDrawers`: Issue with the cone mask fixed.
- `Minimap`: The `MinimapPlanLocation` will now use the actor's Z position by default to prevent mistakes caused by the `TextureGenerator` position.

**Documentation**

- `First Setup`: Added an issues section.
- `Minimap`: Updated the documentation.
- `Drawing Entity`: Added the TeamMask explanation.
- `StealthArea`: Added the FogType explanation.

**Next Features to Come**

- `Rendering` feature should come next.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_