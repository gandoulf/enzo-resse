# **Class: `FFOW_DebugRenderSceneProxy`**

```cpp
class FFOW_DebugRenderSceneProxy
    : public FDebugRenderSceneProxy;
```

---



---

# **Properties**

* # __`CustomShowFlagIndex`__

    ```cpp
    public:
    uint32 CustomShowFlagIndex;
    ```
    
    ---
    
    Optional custom viewport show flag gating this proxy. INDEX_NONE (default) means "always shown"
    so existing users (e.g. the Floor visualiser) are unaffected; the collider visualiser sets it to
    FOW_GetColliderShowFlagIndex() so it only draws when the "Fog Of War Colliders" show flag is enabled.
    




---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_