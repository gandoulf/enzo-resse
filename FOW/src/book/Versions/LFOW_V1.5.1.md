# LFOW V1.5.1

This update fixes a crash caused by `Child Actors`. `Visibility Entities` can now check the fog state using a defined geometry.

## **Feature**

- `Visibility Entities`: Visibility can now be updated based on a geometry shape.

## **Optimization**

- `Visibility Entities`: Improved performance of AABB fog state checks.

## **Fixes**

- `Child Actors`: Packaged games no longer crash when a child actor is present in the level.

## **Documentation**

- `Visibility Entities`: Updated documentation to explain the different update strategies: `Location`, `AABB`, and `Geometry`.
- `Save Load`: New documentation regarding the Save Load system.

## **Next Features to Come**

- `R&D`: Currently experimenting with several ideas.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_