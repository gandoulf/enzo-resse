# **Class: `IFOW_DrawingEntity_Interface`**

```cpp
class FOGOFWAR_API IFOW_DrawingEntity_Interface
    : public IFOW_Entity_Interface;
```

---

Drawing entity used to modify the state of the fog depending of the given [**`UFOW_LayerSetting`**](/reference/classes/UFOW_LayerSetting.md)

> - Override GetEntityLayerSetting to give the correct layer setting
> - Call SetEntityTeam to change the entity team in case of multiplayer game

Contained by : [**`UFOW_Drawer_Shared`**](/reference/classes/UFOW_Drawer_Shared.md)

For more information of the entity virtual fonction please see [**`IFOW_Entity_Interface`**](/reference/classes/IFOW_Entity_Interface.md).


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_