# **Class: `UFOW_Rasterizer`**

```cpp
class FOGOFWAR_API UFOW_Rasterizer
    : public UObject;
```

---

**_Reflection-enabled_**

### Specifiers:
- **abstract**

---

The rasterizer convert the geometries to a bit mask texture representing the state of the FOW.<br />
The reasterizer is never instantied, the default object is always used witch means that you cannot use variable in the class

> - Change the rasterization process by creating a new [**`UFOW_Rasterizer`**](/reference/classes/UFOW_Rasterizer.md) and by changing the default class used in the [**`UFOW_LayerSetting`**](/reference/classes/UFOW_LayerSetting.md)


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_