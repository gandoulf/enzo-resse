# **Class: `UFOW_EntityVisibilityHandler`**

```cpp
class FOGOFWAR_API UFOW_EntityVisibilityHandler
    : public UObject;
```

---

**_Reflection-enabled_**

---

Update the visibility of every registered object implementing IFOW_VisibilityEntity_Interface.<br />
The class is instantied twice in every [**`UFOW_Floor`**](/reference/classes/UFOW_Floor.md) for Static and dynamic entity.<br />
Each entity will query the FOW state at location or for an AABB on the owner FOW_Floor.<br />

> - Change the visibility system by creating a new [**`UFOW_EntityVisibilityHandler`**](/reference/classes/UFOW_EntityVisibilityHandler.md) and by changing the default class used in the [**`AFOW_Handler`**](/reference/classes/AFOW_Handler.md)
> - Override OnVisibilityStateChanged methode in IFOW_VisibilityEntity_Interface to apply custom modification
> - Bind your object to OnVisibilityChanged if you are using FOW_VisibilityComponent

Contained by : [**`UFOW_Floor`**](/reference/classes/UFOW_Floor.md)

---

# **Properties**

* # __`VisibleEntities`__

    ```cpp
    protected:
    TArray<TScriptInterface<IFOW_VisibilityEntity_Interface>> VisibleEntities;
    ```
    
    ---
    
    **_Reflection-enabled_**
    
    ### Specifiers:
    - **BlueprintReadOnly**
    - **Category** = _Internal_
    
    ---
    
    Hold the visible entity
    



---

# **Methods**

* # __`PrepareForWorldDestruction`__

    ```cpp
    public:
    virtual void PrepareForWorldDestruction();
    ```
    
    <details>
    
    ---
    
    **_Reflection-enabled_**
    
    ### Specifiers:
    - **BlueprintCallable**
    - **Category** = _Core_
    
    ---
    
    Call before the world destruction to prevent all Remove or Add operation
    
    </details>
    

* # __`UpdateVisibilityState`__

    ```cpp
    public:
    virtual void UpdateVisibilityState(
        const UFOW_Floor* Floor,
        uint8 FOWGlobalSettingFlags
    );
    ```
    
    <details>
    
    ---
    
    **_Reflection-enabled_**
    
    ### Specifiers:
    - **BlueprintCallable**
    - **Category** = _Core_
    
    ---
    
    Update the visibility state of all registered entity
    
    ---
    
    # **Arguments**
    
    * ## __`Floor`__
    
        ```cpp
        const UFOW_Floor* Floor
        ```
        
        
        
    
    * ## __`FOWGlobalSettingFlags`__
    
        ```cpp
        uint8 FOWGlobalSettingFlags
        ```
        
        
        
    
    
    
    </details>
    




---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_