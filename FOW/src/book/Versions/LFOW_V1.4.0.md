# LFOW V1.4.0

The plugin is now considered stable and has officially left its beta status!  
Version `1.4.0` includes new features, with a major one called `SubFogTexture`, along with retakes, fixes, and updated documentation.

> **/!\ Please check the retake and ensure you update your project with the provided instructions. <br />**

## **Features**

- `Sub Fog Texture`: Generates a sub-fog texture to improve GPU performance when querying the fog state. When enabled, all materials
will have a cheaper execution time.
- `Distance Field Fog`: Channels using the heat texture can have different propagation speeds depending on the world position of the pixel.
- `Stylized Fog`: A fake volumetric fog can be turned ON in the PostProcess to add fog in areas without sight.

## **Retakes**

- `Floor Extended`: The floor extension is now using a `FVector2D`. Be cautious with the update, as all floor setups will be reset. Please
transition first with LFOW V1.3.1 before updating to this version.
- `Materials`: All `Surface`, `PostProcess`, and `User Interface` materials have been updated due to the SubFog feature, and the code has been cleaned.  
Duplicated or custom materials using fog states will need to be updated refer to `M_FOW_OpacityMask`.
- `Fog Computation`: The `Seen` and `Sight` channels have been dissociated in the `Tile`. If the `LayerSetting` option `RevealSight` was set
to true, the `Seen` channel would have been automatically revealed. This no longer applies you will need to set both options to true: `RevealFog` and `RevealSight`.
- `Minimap`: A hard coded 90 degree rotation has been removed. If you are using the minimap, manually add a 90 degree rotation in the `TextureRotationConst`.

## **Fixes**

- `DirectX11 SM5`: Fixed HLSL code compilation for DirectX11.
- `HeatTexture`: Fixed heat remanence when an entity leaves a tile.
- `HeatTexture`: Fixed heating synchronization with the frame rate.
- `Texture Sample Frustum`: Fixed the `CameraOverride`. The game fog sample can now use a custom camera as a reference to update the GPU fog texture.
- `Entities`: All entities are now blueprintable.
- `FOV Entities`: Fixed crash when the radius was larger than the `Floor`.
- `Minimap`: Fixed the render when a floor had different X & Y extents.
- `Replication`: Fixed network saturation caused by fog replication.

## **Documentation**

- `Sub Fog Texture`: New documentation explaining how to enable GPU optimization.
- `Post Process`: Updated documentation with Distance Field and Stylized fog information.

## **Next Features to Come**

- `Navigation`: The fog state will affect AI pathfinding.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_