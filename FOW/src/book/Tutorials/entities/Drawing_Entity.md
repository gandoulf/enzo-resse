# Drawing entity

- [Drawing Entity Components](#drawing-entity-components)
- [Drawing Entity cpp implementation](#drawing-entity-cpp-implementation)

This tutorial has been realised in the `Tutorial/Maps/TutorialMap_Entities` map providen in the
[Demo Project](https://github.com/gandoulf/LayeredFOW_Demo)

# Drawing Entity Components

There is Multiple `DrawingEntity` component implementing the `IFOW_DrawingEntity_Interface`, three different
kind of them exist for now.
* `Geometry drawers`, they will pierce fog by rasterzing a given geometry. used by `FOW_DrawingEntity_BoxComponent`
* `Circle drawers`, they will pierce fog with specific rasterizer only able to trace circle. used by `FOW_DrawingEntity_CircleComponent`
* `FOV drawers`, they will pierce fog by collecting the colliders to create shadow geometries. used by `FOW_DrawingEntity_FOVComponent`

All `DrawingEntity` work the same, they hold data and the given `UFOW_LayerSetting` will define
how this data will be used to pierce the Fog.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/0_DefaultDrawingSetupMerged.png)

To use them add a `FOW_DrawingEntity_CircleComponent` / `FOW_DrawingEntity_BoxComponent` / `FOW_DrawingEntity_FOVComponent` 
to an instanced actor or to your existing `Blueprint`. the Default settings of those component are made to pierce the fog.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/1_AddingDrawingCircleToActor.png)

All drawers will have barelly the same settings.
* `IsEnableAtStart`, define if the entity start drawing from the BeginPlay or if it will be enable later by calling `EnableEntity()`
* `TeamIndexAtStart`, define for which team will the entity be drawing for. The team can be changed at runtime by calling `SetEntityTeam()`
* `Static/DynamicLayerSettingClass`, define how the drawer will bring modification to the fog. Those can't be changed at runtime.
* The advanced section is only necessary for multiple `FOW_Floor` games. There behavior will be explain later.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/2_DrawingEnitySettingsOverView.png)

# Drawing Entity cpp implementation

You can make your own drawing component or directly turn your `UObject` to entities and give them
the possibility to alter the state of the fog. To be done ...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_