# **Class: `UFOW_Floor`**

```cpp
class FOGOFWAR_API UFOW_Floor
    : public UObject;
```

---

**_Reflection-enabled_**

### Specifiers:
- **EditInlineNew**

---

The floor is an area where a bit mask texture is generated to create fog.<br />
Each floor bit mask will be sliced and attributed to a **`TFOW_Tile_Base`**.<br />
It's responsible of the fog state update by querying the fog chunk of every drawer.<br />
Every levels can have many instances of floor to allow verticallity for your game.<br />
Each floor has a collision handler static and dynamic and is responsible for the collision update.<br />

> - Change the collision system by creating a new [**`UFOW_CollisionHandler`**](/reference/classes/UFOW_CollisionHandler.md) and by changing the default class used in the [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)
> - Change the visibility system by creating a new [**`UFOW_EntityVisibilityHandler`**](/reference/classes/UFOW_EntityVisibilityHandler.md) and by changing the default class used in the [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)

Contained by : [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)

Warning : supperposed floor will work correctly only if you change the PP material in [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_