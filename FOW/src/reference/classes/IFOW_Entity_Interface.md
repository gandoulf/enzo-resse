# **Class: `IFOW_Entity_Interface`**

```cpp
class FOGOFWAR_API IFOW_Entity_Interface;
```

---

Base class for every entity interface, [**`IFOW_GeometryEntity_Interface`**](/reference/classes/IFOW_GeometryEntity_Interface.md) is an exception subject to a retake

> - [**`IFOW_DrawingEntity_Interface`**](/reference/classes/IFOW_DrawingEntity_Interface.md)
> - [**`IFOW_CollisionEntity_Interface`**](/reference/classes/IFOW_CollisionEntity_Interface.md)
> - [**`IFOW_VisibilityEntity_Interface`**](/reference/classes/IFOW_VisibilityEntity_Interface.md)

Entities are by default automatically updated by the system if (IsStatic == false && FloorVolatile)
> - FloorVolatile express the posibility to move from a floor to another

Contained by : [**`UFOW_EntityContainer`**](/reference/classes/UFOW_EntityContainer.md)

Warning : every multiple inheritance have specifique overriding rule regarding methodes finishing by _M.<br />
You can use **`AFOW_CustomCollision`** as examble for your custom entity implementation


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_