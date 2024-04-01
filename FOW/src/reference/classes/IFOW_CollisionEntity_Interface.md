# **Class: `IFOW_CollisionEntity_Interface`**

```cpp
class FOGOFWAR_API IFOW_CollisionEntity_Interface
    : public IFOW_Entity_Interface;
```

---

Collision entities are the sight blocker to prevent fog discovering between rooms.<br />
By design any child implementing this class should also implement [**`IFOW_DrawingEntity_Interface`**](/reference/classes/IFOW_DrawingEntity_Interface.md) to enable optimisation

> - Depending of the situation you can have issues because of collision drawing optimisation, Override ShouldDrawColliders and return false to disable it
> - You can disable the whole collision drawing optimisation by disabling DrawFOWCollider in [**`UFOW_LayerHandler`**](/reference/classes/UFOW_LayerHandler.md)

Contained by : [**`UFOW_CollisionHandler`**](/reference/classes/UFOW_CollisionHandler.md)

For more information of the entity virtual fonction please see [**`IFOW_Entity_Interface`**](/reference/classes/IFOW_Entity_Interface.md).


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_