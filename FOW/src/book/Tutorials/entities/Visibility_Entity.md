# Visibility entity

- [Visibility Entity Component](#visibility-entity-component)
- [Visibility Entity cpp implementation](#visibility-entity-cpp-implementation)

This tutorial has been realised in the `Tutorial/Maps/TutorialMap_Entities` map providen in the
[Demo Project](https://github.com/gandoulf/LayeredFOW_Demo)

# Visibility Entity Component

This component implement `IFOW_VisibilityEntity_Interface` and allow your game to change the
visibility of your actors depending of the fog state.

![VisibleEntity](../../../Assets/Tutorial/Entities/Visibility/0_MergePictureVisibilityComponent2.png)

To use it add a `FOW_VisibilityEntity_Component` to an instanced actor or to your existing `Blueprint`.
the component will by default hide the actor if not in sight.

![VisibleEntity](../../../assets/Tutorial/Entities/Visibility/1_AddVisibleEntityToActor.png)

To go a bit further, if you whant to apply custom code when the visibility state change, you can implement
the `OnVisibilityChanged` event from the component in your `Blueprint`.

![VisibleEntity](../../../assets/Tutorial/Entities/Visibility/2_CustomVisibilityUpdate.png)

By default the FOW state is return as a uint8, it doesn't means a lot for you but it is a mask representing
the 8 chanels. You can transform it to a more readable enum by calling `GetFOWStateFromBits`. Now just
switch on the returned enum to apply your custom code. For the example I'm juste drawing debug sphere.

![VisibleEntity](../../../assets/Tutorial/Entities/Visibility/3_DrawDebugSphereOnVisibilityChanged.png)

And here you go, green sphere appear when the actor is reveald, and a red one appear when the player
loose sight on it.

![VisibleEntity](../../../assets/Tutorial/Entities/Visibility/4_DrawDebugSphereForVisibility.png)

If the popping render displease you, you can turn it off by unchecking `DisableRenderOutSight`. if you do
so nothing will happen anymore and you will have to do the magic by yourself, material translusency transition
or an explosion maybe ? :)

![VisibleEntity](../../../assets/Tutorial/Entities/Visibility/5_DisablePremadeVisibilityEffect.png)

# Visibility Entity cpp implementation

You can make your own visibility component or directly turn your `UObject` to entities and give them
the possibility to react to the Fog state. To be done ...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_