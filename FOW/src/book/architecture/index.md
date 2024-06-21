# Architecture

This section will explain in-depth how the Fog Of War has been thought out. It'll give you the keys to tweak
everything and set up the plugin to fit your game the best possible way.

Keep in mind that the Layered FOW doesn't need any modification to be used in game; only if performances are
an issue, modifications will be necessary.

## Everything is Tile-shaped

To allow high precision and large scale game, everything has been cut into pieces which can be seen as tiles.
This tiling system is really efficient for optimization and multithreading. The FOW is designed this way:
* `FOWHandler`: the biggest piece holding every data. It's a singleton, and only one instance can exist in the level.
* `FOWFloors`: 3D boxes held by the Handler, where the fog will be applied. There is no number or position limitation. It will store a bits array of the fog state and everything necessary to generate fog fragment.
* `FOWTiles`: Defined by a power of 2 of fog pixels, it will create a grid for every element interacting with the fog. Used to merge fog fragment to the result texture in the Floors.
* `FOWTextureSample`: The bond between CPU and GPU, it will collect Floors bit array to send it to the GPU via a texture.

## The logic is managed by Entities

The Entities are a suite of interfaces allowing data generation or querying. They are self-dependent and don't
need any update, no API is provided unless two methods to enable/disable the entity. The FOW will do all the
updates it needs to correctly generate the fog state of the frame. Entities exist in 3 different forms inheriting
from a base interface, plus one a bit different, designed for a late purpose:
* `CollisionEntity`: Provide methods to gather collision from an object. Collisions are used by the drawers to cast shadow. The entity will be stored in CollisionHandler.
* `DrawingEntity`: Provide methods to collect drawing settings from an object. The entity will be registered to shared drawer to generate fog fragment.
* `VisibilityEntity`: Provide methods to collect object size and location to update its visible state depending on the fog.
* `GeometryEntity`: It doesn't derive from the Entity base class; its purpose is to hold geometry data to be used by entities (calling it GeometryEntity was a mistake).

> **/!\ The links under apparently don't work, I'm trying to figure it out, please use the links on the left <br />**

# Pages

- [Handler](/book/architecture/Handler.md)
- [Floor](/book/architecture/Floor.md)
- [Layers](/book/architecture/Layers.md)

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_