# LFOW V1.3.0

UE 5.5 compatibility, Rendering features, Fixes, documentation

> **/!\ Please check the retake and ensure you update your project with the provided instructions. <br />**

**Features**

- `Unreal Engine v5.5`: The plugin supports the upcoming version of Unreal.
- `Texture assets`: Fog game texture can now be assets, allowing any material to use it and create logic based on the fog state.
- `Custom depth buffer`: Assets can be rendered in a different stencil to ignore the fog.
- `Entity sight mask`: FOV entities can have a cone mask.
- `Floors area`: Floors now use a `Vector2D` to define their bounds, providing more precise fog delimitation.
- `Visibility fade`: Adds `UFOW_VisibilityE_FadeComponent` to fade in/out material rendering.
- `FOV Drawers event`: FOV drawers will now trigger an event when they enter or leave a floor: `OnDrawerEnterFloor` & `OnDrawerLeaveFloor`.
- `Plugin ensure`: Ensures can now be disabled by setting `USE_FOW_ENSURE` to 0; be certain of your implementation before turning it off.

**Retakes**

- `Floors`: `FloorExtend` is now deprecated, use the FVector2D `FloorExtends` to set the floor size. The pink plane display is disabled by
default; an orange limit will show the actual fog position.
- `Minimap`: Numerous fixes have been applied to the minimap. A 90 degree rotation may appear on some minimaps. Please use `TextureRotationConst` to correct it.

**Fixes**

- `Linux compilation`: Fixes header include.
- `ARM64`: Implementation of NEON to replacce 128-bit SIMD instructions (requires testing, environment-dependent).
- `Drawers`: Adds functions to enable/disable drawers without querying `FOWHandler`: `AddDrawerToHandler` and `RemoveDrawerFromHandler`.
- `FOWHandler crash`: Plugin no longer crashes when `FOWHandler` is absent.
- `Network`: Removing the `NetworkSettings` for online games works correctly. Enabling game setup without replication dependency from the FOW.
- `Minimap`: Fixes fog pixel strips on some minimaps.
- `Minimap`: Fixes rotation, displacement and scale.
- `Stealth Area`: Area cluster reconstruction time optimized (previously 17 ms for 10 areas in contact).

**LayeredFOW_Demo:**

- The project has been updated with new tutorials and my custom minimap implementation, which supports widgets. Feel free to use it; however,
support won't be provided. See the `MinimapWithIcon` folder and check the `TutorialMap_Minimap_Icon` map where everything is set up.

**Documentation**

- `Material Opacity`: New rendering tutorial.
- `Stencil`: New rendering tutorial.
- `First Setup`: Updated tutorial, explanation over the difference between `FOVEntities` and `FOVDrawers`.
- `Visibility Entity`: Updated tutorial to include the fade component.

**Next Features to Come**

- `Rendering` feature is upcoming.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_