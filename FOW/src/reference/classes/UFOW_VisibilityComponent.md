# **Class: `UFOW_VisibilityComponent`**

```cpp
class FOGOFWAR_API UFOW_VisibilityComponent
    : public UActorComponent
    , public IFOW_VisibilityEntity_Interface;
```

---

**_Reflection-enabled_**

### Meta Specifiers:
- **BlueprintSpawnableComponent**

---

Can be added to any actor which need to be hidden when the player hasn't sight on it

> - Enable IsEntityFloorVolatile to use the default visibility update
> - Bind yourself to OnVisibilityChanged to customise the visibility update

Contained by : [**`UFOW_EntityVisibilityHandler`**](/reference/classes/UFOW_EntityVisibilityHandler.md)

---

# **Properties**

* # __`OnVisibilityChanged`__

    ```cpp
    public:
    FOnVisibilityChanged OnVisibilityChanged;
    ```
    
    ---
    
    **_Reflection-enabled_**
    
    ### Specifiers:
    - **BlueprintAssignable**
    - **BlueprintCallable**
    - **Category** = _FOW_
    
    ---
    
    Called every time the Visibility state has changed
    




---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_