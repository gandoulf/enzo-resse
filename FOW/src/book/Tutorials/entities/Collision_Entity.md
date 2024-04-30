# Collision entity

- [Collision Entity Component](#collision-entity-component)
- [Collision Entity C++ Implementation](#collision-entity-cpp-implementation)

This tutorial has been realized in the `Tutorial/Maps/TutorialMap_Entities` map provided in the [Demo Project](https://github.com/gandoulf/LayeredFOW_Demo).

## Collision Entity Component

There are multiple `CollisionEntity` components implementing the `IFOW_CollisionEntity_Interface`. All collisions
work the same; they store geometry that will be given to a `UFOW_CollisionHandler`. The handler will then provide
query class to collect collider information. The geometry can be convex and concave; it's only required to correctly
sort the vertices.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/0_SetupCollisionComponentMerged.png)

To use them, add a `FOW_CollisionEntity_BoxComponent` or `FOW_CollisionEntity_CustomComponent` to an instanced actor
or to your existing blueprint. I use for the example the box component; if you want to use the custom component to
generate custom collision, you will have to provide vertices.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/2_AddBoxCollisionComponent.png)

Select the `FOW_CollisionEntity_BoxComponent` and reset the scale to 1.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/3_ResetCollisionBoxScaleToOne.png)

If you take a look at the collision entity settings, you will see that `Static/DynamicLayerSettingClass` are required.
It's the case because colliders are also `DrawingEntities`; their geometry can be drawn on a fog fragment by a drawer
as an optimization if `ShouldBeDrawn` is checked. See the [Layer tutorial](/book/Tutorials/entities/../Layers.md) for more information.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/4_CollisionEntityGeneralParameters.png)

Collisions are subject to heavy update time in every game. It is the same for the FOW; collision takes time to query.
To optimize those queries, we're using acceleration structures that are super fast; however, their update or construction
time might be heavy. To overcome this issue, we split static colliders from dynamic. It's really important for your game
to have actors set correctly to `static` or `movable` depending on your needs. Static collision is significantly faster
than dynamic.

![CollisionEntity](../../../Assets/Tutorial/Entities/Collision/5_SetCollidersMobilityToStatic.png)

## Collision Entity C++ Implementation

You can make your own collision component or directly turn your `UObject` to entities and give them the possibility to
block the sight of drawers. To be done...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_