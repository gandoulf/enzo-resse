# Visibility Entity

- [Visibility Entity Components](#drawing-entity-components)
	- [Default entity](#default-entity)
	- [Fading entity](#fading-entity)
- [Visibility Entity cpp implementation](#visibility-entity-cpp-implementation)

This tutorial has been realized in the `Tutorial/Maps/TutorialMap_Entities` map provided in the [Demo Project](https://github.com/gandoulf/LayeredFOW_Demo).

## Visibility Entity Components

This components implement `IFOW_VisibilityEntity_Interface` and allows your game to change the visibility
of your actors depending on the fog state.

![VisibilityEntityComponent](../../../Assets/Tutorial/Entities/Visibility/0_MergePictureVisibilityComponent2.png)

### Default entity

To use it, add a `FOW_VisibilityEntity_Component` to an instanced actor or to your existing Blueprint.
The component will by default hide the actor if it is not in sight.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/1_AddVisibleEntityToActor.png)

To go a bit further, if you want to apply custom code when the visibility state changes, you can implement
the `OnVisibilityChanged` event from the component in your Blueprint.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/2_CustomVisibilityUpdate.png)

By default, the FOW state is returned as a uint8, which doesn't mean much for you, but it is a mask
representing the 8 channels. You can transform it to a more readable enum by calling `GetFOWStateFromBits`.
Now just switch on the returned enum to apply your custom code. For example, I'm just drawing a debug sphere.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/3_DrawDebugSphereOnVisibilityChanged.png)

And here you go, a green sphere appears when the actor is revealed, and a red one appears when the player
loses sight of it.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/4_DrawDebugSphereForVisibility.png)

If the popping render displeases you, you can turn it off by unchecking `DisableRenderOutSight`. If you
do so, nothing will happen anymore, and you will have to do the magic by yourself, perhaps a material
translucency transition or an explosion?

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/5_DisablePremadeVisibilityEffect.png)

### Fading Entity

The default visibility component might not be sufficient for high-quality rendering. There is an alternative component
that allows a dynamic material to fade in and out. The drawback of this system is that it uses dynamic materials, which
can be slightly heavier on the render pipeline. Let's set up the component in the `Tutorial/Maps/TutorialMap_Entities` to
create a fade render effect like the one in the feature showcase.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/6_VisibilityEntity_Fading.png)

Open the `BP_VisibleInGameElement_Fade` and add a `FOW_VisibilityEntity_FadeComponent`; it will be responsible for updating
the material parameters throughout the tick (only active when fading).

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/7_AddFadingComponent.png)

Now, in the `Construction Script`, add a few nodes to set up the component:
- Use `CreateDynamicMaterialInstance` for the StaticMesh and set the `Source Material` to `M_FOW_Visibility_Dithering`, which is included in the plugin.
- Use the return value to create an array of materials.
- Get the `Visibility Component`, call `AddMaterialToFade`, and provide the array of materials that need to fade.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/8_AddConstructorCode.png)

If you check the `Visibility Component` details, you will find the default variables of a `Visibility Entity` plus two new variables:
- `FadeAmount`: Allows you to change the fading level in your scene to preview how it will render. This will reset when the game starts.
- `FadeTime`: The duration of the fade in/out effect.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/9_ComponentSettings.png)

If you open `M_FOW_Visibility_Dithering`, you will find all the necessary nodes to replicate this fading effect on any material.

![VisibilityEntityComponent](../../../assets/Tutorial/Entities/Visibility/10_MaterialNodeForFading.png)

## Visibility Entity cpp implementation

You can make your own visibility component or directly turn your `UObject` into entities and give them
the possibility to react to the Fog state. To be done ...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_