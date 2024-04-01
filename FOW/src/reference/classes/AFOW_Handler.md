# **Class: `AFOW_Handler`**

```cpp
class FOGOFWAR_API AFOW_Handler
    : public AActor;
```

---

**_Reflection-enabled_**

### Specifiers:
- **abstract**

---

The Fog Of War Handler is the base class of the plugin, it's a sigleton and you cannot have many instance of it even when doing networked game with replication<br />
The Fog Of War is highly parametrable and let the developers override almost everything. You might want to get ride of some functionality or maybe to write a more optimized code<br />
The handler hasn't any main logic, it's purpose is to:
- Have general settings
- Initialise FOW Object
- Run the update
- Contain FOW element instancies

You have the possibility to change the core module of the FOW by changing the default class used int the settings

> - If you want a custom FOWHandler be sure to override FindLevelFOWHandler, you can use **`AFOW_Handler_Default`** as example
> - Go to the FOWFloors settings and display the parametters to shape the floor to your needs


---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_