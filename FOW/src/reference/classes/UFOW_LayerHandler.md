# **Class: `UFOW_LayerHandler`**

```cpp
class FOGOFWAR_API UFOW_LayerHandler
    : public UObject;
```

---

**_Reflection-enabled_**

### Specifiers:
- **Blueprintable**

---

The layer handler allow you to change the computation order of the different [**`UFOW_LayerSetting`**](/reference/classes/UFOW_LayerSetting.md)

> - Layer will modify the fog state in the given order, which means that a modification can be overriden by an other layer
> - Enable or disable the collision drawing optimisation by changing DrawFOWCollider


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_