# LFOW V1.5.0

This update brings Android support to LFOW! In addition, two new material static parameters have been added to reduce GPU usage.

## **Feature**

- `Android`: LFOW is now compatible with Android devices.

## **Optimization**

- `GPU`: A new option is available in `MPP_FOW_Floor` to work with a single floor only, speeding up computation.
- `GPU`: A new option is available in `MPP_FOW_Floor` to use a lightweight version of the blur, reducing dynamic branching.

## **Fixes**

- `Materials`: Fix the Channel value when not used, set to 1.
- `NEON`: All Neon SIMD instructions are now correctly implemented using `sse2neon.h`.
- `Replication`: Fix crash when a none existing channel is replicated. (eg 2 channel per team and the third one is asked to be replicated)

## **Documentation**

- `Android`: Added setup instructions to enable LFOW in mobile projects. The documentation also applies to console and laptop platforms if you need improved performance.

## **Next Features to Come**

- `R&D`: Currently experimenting with several ideas.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_