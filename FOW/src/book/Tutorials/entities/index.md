# Fog of war Entities

Entities system are used by default as a solution to memory fragmentation causing heavy update.
It has been designed with this fact in mind but also to let anything be part of the FOW. Entities
are collected and stored under containers to keep requiered data for the system update. They
inherite from `UFOW_Entity_Interface` which is a `UInterface`. I'm using the unreal interface
implementation to allow callable functions for Blueprint only users. The downside of it is that
entities has to be at least a `UObject`.<br />

The Entities can be implemented only in the C++ side, However many predifined `Actor` and
`ActorComponent` are providen with already implemented interface. You will find in
those derived class two function allowing you to `EnableEntity()` or `DisableEntity()` anywhere
at anytime. There is no other API, they are self suffisante and their update are managed by
the containers.


# Pages

- [Visibility entity](/book/Tutorials/entities/Visibility_Entity.md)
- [Drawing entity](/book/Tutorials/entities/Drawing_Entity.md)
- [Collision entity](/book/Tutorials/entities/Collision_Entity.md)

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_