# **Class: `UFOW_VisibilityE_Component`**

```cpp
class FOGOFWAR_API UFOW_VisibilityE_Component
    : public UActorComponent
    , public IFOW_VisibilityEntity_Interface;
```

---

**_Reflection-enabled_**

### Specifiers:
- **ClassGroup** = _Entity_

### Meta Specifiers:
- **BlueprintSpawnableComponent**
- **DisplayName** = _FOW_VisibilityEntityComponent_

---

Can be added to any actor which need to be hidden when the player hasn't sight on it

> - Enable IsEntityFloorVolatile to use the default visibility update
> - Bind yourself to OnVisibilityChanged to customise the visibility update

Contained by : [**`UFOW_EntityVisibilityHandler`**](/reference/classes/UFOW_EntityVisibilityHandler.md)

---

# **Properties**

* # __`OnEntityStealthStateChanged`__

    ```cpp
    public:
    FEvent_VisibleEntityStealthState OnEntityStealthStateChanged;
    ```
    
    ---
    
    **_Reflection-enabled_**
    
    ### Specifiers:
    - **BlueprintAssignable**
    - **BlueprintCallable**
    - **Category** = _FOW_
    
    ---
    
    Called every time the the entity enter/leave stealth area
    

* # __`OnVisibilityChanged`__

    ```cpp
    public:
    FOnVisibilityChangedd OnVisibilityChanged;
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