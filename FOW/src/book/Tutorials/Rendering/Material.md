# Post Process

- [Change fog render](#change-fog-render)

This tutorial is about changing the fog render, you can use any map that you want.

## Change fog render

A FOW is a heavy piece of code, but the rendering is managed by a single material. All the information is sent
via textures, with three currently in use:
- `Floor data`, holding position, extend, texture offsets
- `Floor fog state`, holding the visibility state of the fog
- `Floor fog heat state`, allow fog lerp between two frame state (only used if enabled)

The material is designed to hide the more difficult parts within material functions to make it less overwhelming,
but you are welcome to read and modify anything you want (though it might be a challenging task).<br/>
The rest of the material should be straightforward and will let you tweak the fog rendering for your projects!

> **/!\ The `MPP_FOW_Floors` is used as default for the tutorial, but you might be using the
`MPP_FOW_FloorsTransparency` if you are implementing a game with verticallity <br />**

Let's try to change the render of the black fog at first, Open the `MPP_FOW_Floors`, it should look like this

![FogRenderPictures](../../../assets/Tutorial/Rendering/Material/1_OpenMPP_FOW_Floors.png)

Add a `Constant4Vector` and plug it into the `Lerp`with a value of 0. Change the constant value of the R channel to 1.

![FogRenderPictures](../../../assets/Tutorial/Rendering/Material/2_ReplacePinA.png)

Press the play button and see the undiscovered area beeing rendered in red.

![FogRenderPictures](../../../assets/Tutorial/Rendering/Material/3_RedFogRender.png)

Now let's see how to bring texture to the grey fog:
- Create a `Noise` and a `Multiply` nodes.
- Bind the noise and the result, and pin the output from the `Lerp` to the new `Multiply`.
- Finally pin the result of the `Multiply` to the entry A of the `Lerp`.
You may need to increase the 0.1 value from the previous Multiply to 0.5 to correctly see the noisy render.

![FogRenderPictures](../../../assets/Tutorial/Rendering/Material/4_MultiplyGreyByNoise.png)

Press the play button, and see areas in sight being rendered in a noisy grey.

![FogRenderPictures](../../../assets/Tutorial/Rendering/Material/5_NoiseFogRender.png)
---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_