# LFOW V1.5.4

This update fixes crashes related to sublevel loading.

## **Features**

- `Initialization`: A `FOW_Subsystem` is now available, fixing many issues with the initialization pipeline. `FOW_GetHandlerInstance_Interface` is now deprecated.
- `Networking`: The `FOW_DelayedInitializer` allows more modular network initialization.
- `Seamless loading`: Levels can be dynamically loaded/unloaded, and all entities will be correctly registered/unregistered.

## **Fixes**

- `Seamless loading`: No longer crashes.

## **Documentation**

- `Networking`: `FOW_GetHandlerInstance_Interface` is now deprecated.
- `Sub Level`: New documentation regarding sublevels.

## **Next Features to Come**

- `Render`: New fog rendering

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_