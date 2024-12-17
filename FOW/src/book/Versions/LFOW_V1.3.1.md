# LFOW V1.3.1

Material Opacity Fix for packaged project

> **/!\ Please check the retake and ensure you update your project with the provided instructions. <br />**

**Retakes**

- `Material Opacity`: Removing `MPC_FOW_VFXRenderSettings` and inserting parameters in the `MPC_FOWRenderSettings`. Materials can only have
up to 2 collections. With the MPC removed, materials created with the node from V1.3.0 might break and need an `MPC` replacement. 

**Fixes**

- `Material Opacity`: Now working for the packaged project.
- `Feature showcase map`: Updated with new rooms showing material opacity and stencil.

**Documentation**

- `Material Opacity`: Updated documentation due to the retake.
- `Drawing Entity`: Added a new paragraph for the FOV cone mask.
- `PluginAPI`: New documentation providing knowledge on the useful functions within the plugin.

**Next Features to Come**

- `Rendering`: Volumetric fog material.
- `Rendering`: Blur quality.
- `Optimization`: Post-process compute time.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_