# Collision entity

- [Collision Entity Component](#collision-yentity-component)
- [Collision Entity cpp implementation](#collision-entity-cpp-implementation)

This tutorial has been realised in the `Tutorial/Maps/TutorialMap_Entities` map providen in the
[Demo Project](https://github.com/gandoulf/LayeredFOW_Demo)

# Collision Entity Component

There is Multiple `CollisionEntity` component implementing the `IFOW_CollisionEntity_Interface`.
All collision work the same, they store a geometry that will be given to a `UFOW_CollisionHandler`.
The handler will then profide query class to collect colliders informations. <br />
The geometry can be convex and concave, it's only requiered to correctly sort the vertices.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/0_SetupCollisionComponentMerged.png)

To use them add a `FOW_CollisionEntity_BoxComponent` or `FOW_CollisionEntity_CustomComponent`
to an instanced actor or to your existing `Blueprint`. I use for the example the box component,
if you wanna use the custom component to generate custom collision you will have to provide vertices.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/2_AddBoxCollisionComponent.png)

Select the `FOW_CollisionEntity_BoxComponent` and reset the scale to 1.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/3_ResetCollisionBoxScaleToOne.png)

If you take a look to the collision entity `settings` you will see that `Static/DynamicLayerSettingClass` are requiered.
It's the case because colliders are also `DrawingEntities`. If `ShouldBeDrawn` is check and if the
`UFOW_LayerHandler` is correctly set colliders will provide their geometries to a `UFOW_Drawer_Shared`.
It's present as an optimisation for maps with a lots of `FOVDrawers` or `FOVEntities`, it'll allow the
FOW to rasterize the colliders geometry into a static layer which will reduce the triangle count per geometry
for dynamic drawing.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/4_CollisionEntityGeneralParameters.png)

Hit the play button and see the shape of the collision blocking the sight of the drawer.

# Collision Entity cpp implementation

You can make your own collision component or directly turn your `UObject` to entities and give them
the possibility to block the sight of drawers. To be done ...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_