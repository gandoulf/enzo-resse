# Drawing entity

- [Drawing Entity Components](#drawing-entity-components)
- [Drawing Entity Cpp implementation](#drawing-entity-cpp-implementation)

This tutorial has been realized in the `Tutorial/Maps/TutorialMap_Entities` map provided in the [Demo Project](https://github.com/gandoulf/LayeredFOW_Demo).

## Drawing Entity Components

There are multiple `DrawingEntity` components implementing the `IFOW_DrawingEntity_Interface`. Three different kinds of them exist for now:
* `Geometry drawers`: They will pierce fog by rasterizing a given geometry. Used by `FOW_DrawingEntity_BoxComponent`.
* `Circle drawers`: They will pierce fog with a specific rasterizer only able to trace circles. Used by `FOW_DrawingEntity_CircleComponent`.
* `FOV drawers`: They will pierce fog by collecting the colliders to create shadow geometries. Used by `FOW_DrawingEntity_FOVComponent`.

All `DrawingEntity` work the same; they hold data and the given `UFOW_LayerSetting` will define how this data will be used to pierce the Fog.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/0_DefaultDrawingSetupMerged.png)
![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/1_AddVisibleEntityToActor.png)

To use them, add a `FOW_DrawingEntity_CircleComponent` / `FOW_DrawingEntity_BoxComponent` / `FOW_DrawingEntity_FOVComponent` to an instanced
actor or to your existing `Blueprint`. The default settings of those components are made to pierce the fog.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/1_AddingDrawingCircleToActor.png)

All drawers will have barely the same settings:
* `IsEnableAtStart`: Define if the entity starts drawing from the BeginPlay or if it will be enabled later by calling `EnableEntity()`.
* `TeamIndexAtStart`: Define for which team the entity will be drawing. The team can be changed at runtime by calling `SetEntityTeam()`.
* `Static/DynamicLayerSettingClass`: Define how the drawer will bring modification to the fog. Those can't be changed at runtime.
* The advanced section is only necessary for multiple `FOW_Floor` games. Their behavior will be explained later.

![DrawingEntity](../../../Assets/Tutorial/Entities/Drawing/2_DrawingEnitySettingsOverView.png)

## Drawing Entity cpp implementation

You can make your own drawing component or directly turn your `UObject` to entities and give them the possibility to alter the state of the fog. To be done...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_