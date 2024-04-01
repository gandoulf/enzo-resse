# **Class: `UFOW_Tile_Class`**

```cpp
class FOGOFWAR_API UFOW_Tile_Class
    : public UObject;
```

---

**_Reflection-enabled_**

### Specifiers:
- **Abstract**

---

**`TFOW_Tile_Base`** aren't a UCLASS to prevent saturation of GC, thus they are all wrapped by a FOW_Tile_Class and allocated the old way.<br />
Tiles are used to compute fog result of the [**`UFOW_DrawerComponent`**](/reference/classes/UFOW_DrawerComponent.md) and merge it depending of the [**`UFOW_LayerSetting`**](/reference/classes/UFOW_LayerSetting.md) under a bit array that will feed the [**`UFOW_TextureSample`**](/reference/classes/UFOW_TextureSample.md) sent to the GPU.<br />
You can simply create your own tile update by overriding this class and by using the templated class **`TFOW_Tile`**.
you will have to create 3 templated classes to finish your fully custom tiles :
- Update
- Compute
- Merge

> - Override GetTileBitsFormat to correctly set the tile pixel number for the FOW
> - Override GetTileChannelNbr to correctly set the channels number per tiles
> - Override GetTilePackagingFormat to correctly set the packaging format use by the FOW

Contained by : [**`UFOW_Floor`**](/reference/classes/UFOW_Floor.md)

Warning : I highly advise to use the EnumFOWTilePackagingFormat::PACKED format for tiles for optimisation reason


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_