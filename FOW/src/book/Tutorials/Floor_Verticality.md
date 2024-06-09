# Floor and Verticality

- [Add Floors](#add-floors)
- [Enable Verticality](#enable-verticality)

This tutorial has been realized in the `Tutorial/Maps/TutorialMap_Floors` map provided in the [Demo Project](https://github.com/gandoulf/LayeredFOW_Demo).

> **The multi-floor feature is in progress and can create undesirable rendering artifacts. Most of them are known and
will be dealt with in the next version. However, you can still prototype your game with it; the system will remain the
same.**

# Add Floors

Floors are the area representation of the fog in the editor. You can add as many as you want, and they are represented
by a yellow rectangle and a pink plane.
* The rectangle represents the fog area; everything inside will be impacted by fog.
* The plane represents the fog extent clamped to tiles. Fog is not constrained to the rectangle for now, but it might
become the case soon. It also dissociates the top from the bottom of the fog when modifying the ZExtend.

To add a new floor, select the `FOW Handler`. In the details panel, find the `FOWFloors` array and add an element.

![AddFloorToMap](../../Assets/Tutorial/Floors_Verticality/1_AddFloorToMap.png)

Find the new element, which should be set to `None`, and change its value to `FOW_Floor`.

![SelectFloorClass](../../Assets/Tutorial/Floors_Verticality/2_SelectFloorClass.png)

In the added element, you will find a `FloorLocation` variable in the settings section, allowing you to change the
position of the floor. Move it so that the other part of the plane is included in the new floor.

![MoveTheFloorInY](../../Assets/Tutorial/Floors_Verticality/3_MoveTheFloorInY.png)

As I mentioned, there are currently a few artifacts between floors around the junctions. You can see sharp fog lines
not affected by blur.

![UndesirableArtifactsAtIntersection](../../Assets/Tutorial/Floors_Verticality/4_UndersirableArtifactsAtIntersection.png)

# Enable Verticality

The fog of war is an algorithm used for 2D gameplay and mostly competitive games like MOBA/RTS. It has been a challenge
to open the door to a new kind of game which could take benefits from verticality.

To use verticality in your game, you have to first change the `PostProcess` used to render the fog. Select the `FOW_Handler`,
in the details panel find the `FOWShaderClass` and change the `MPP_FOW_Floors` to `MPP_FOW_FloorsTransparency`.

![ChangePostProcess](../../Assets/Tutorial/Floors_Verticality/5_ChangePostProcess.png)

Still in the `FOW_Handler`, add 2 new floors and I advise you to change the editor view to `Front`; it'll simplify the
positioning of the floors. As with the previous floor, you will have to change the `FloorLocation`. Try to center the
fog plane to the gameplay area in Y and Z.

![AddThreeFloorsandMoveYZ](../../Assets/Tutorial/Floors_Verticality/6_AddThreeFloorAndMoveYZ.png)

With the default settings, you should have a gap between your floors, and it's better to not have them. Reach the settings
of each floor and change the `Y` value of the `ZExtend`. It'll enlarge the bottom part of the yellow square.

![RemovetheGapBetweenFloors](../../Assets/Tutorial/Floors_Verticality/7_RemoveTheBetweenFloor.png)

One last thing, many settings are provided to the material and one can generate conflict with verticality. To disable it,
select the `FOW_Handler`, in the details panel find the `MPC_FOWRenderSettings` and open it.

![OpenMPC_FOWRenderSettings](../../Assets/Tutorial/Floors_Verticality/8_OpenMPC_FOWRenderSettings.png)

Find the `bEnableHeightGrading` scalar value and set it to 0.

![RemoveHeightGrading](../../Assets/Tutorial/Floors_Verticality/9_RemoveHeightGrading.png)

As explained at the beginning of this tutorial, the multi-floor rendering is still in progress and the vertical transition
hasn't been properly cleaned.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_