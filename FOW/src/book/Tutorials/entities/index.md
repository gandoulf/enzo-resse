# Fog of War Entities

The entities system is used by default as a solution to memory fragmentation causing heavy updates. It has
been designed with this fact in mind but also to allow anything to be part of the FOW. Entities are collected
and stored under containers to keep required data for the system update. They inherit from `UFOW_Entity_Interface`,
which is a `UInterface`. I'm using the Unreal interface implementation to allow callable functions for Blueprint-only
users. The downside of it is that entities have to be at least a `UObject`.

The Entities can be implemented only on the C++ side. However, many predefined `Actor` and `ActorComponent`
are provided with already implemented interfaces. You will find in those derived classes two functions allowing
you to `EnableEntity()` or `DisableEntity()` anywhere at any time. There is no other API; they are self-sufficient,
and their updates are managed by the containers.

> **/!\ The links under apparently don't work, I'm trying to figure it out, please use the links on the left <br />**


# Pages

- [Visibility Entity](/book/Tutorials/entities/Visibility_Entity.md)
- [Drawing entity](/book/Tutorials/entities/Drawing_Entity.md)
- [Collision entity](/book/Tutorials/entities/Collision_Entity.md)

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_