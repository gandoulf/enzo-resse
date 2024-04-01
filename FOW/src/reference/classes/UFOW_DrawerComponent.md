# **Class: `UFOW_DrawerComponent`**

```cpp
class FOGOFWAR_API UFOW_DrawerComponent
    : public UActorComponent;
```

---

**_Reflection-enabled_**

### Specifiers:
- **Abstract**
- **Blueprintable**

---

The drawer component compute fog modification, however it doesn't apply it.<br />
They are small chunk of fog aligned to the world grid, they can be seen as canvas.<br />
Their update are the slowest because of the collision querying and the geometry rasterization.<br />
By default they are mean to be added to each actor modifying the fog however the memory allocation and merging can become very time consuming.<br />
If your game needs higher performance take a look at [**`IFOW_CollisionEntity_Interface`**](/reference/classes/IFOW_CollisionEntity_Interface.md) which will request the creation of a [**`UFOW_Drawer_Shared`**](/reference/classes/UFOW_Drawer_Shared.md) to the system.<br />

It is possible to :
> - Create custom drawer by inheriting from this class and by overriding GenerateDrawerGeometry to inject your custom geometry
> - Change the rasterization process by creating a new [**`UFOW_Rasterizer`**](/reference/classes/UFOW_Rasterizer.md) and by changing the default class used in the [**`UFOW_LayerSetting`**](/reference/classes/UFOW_LayerSetting.md)
> - Change the collision querying by creating a new [**`UFOW_CollisionHandler`**](/reference/classes/UFOW_CollisionHandler.md) and by changing the default class used in the [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)

Contained by : [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_