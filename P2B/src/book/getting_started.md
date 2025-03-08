# Getting Started

## Table of Contents

- [Paint 2 Blocking](#paint-2-blocking)
- [Features](#features)
  - [3D Generation](#3d-generation)
  - [Parametric Generation](#parametric-generation)
  - [Custom Blockers](#custom-blockers)
  - [Painting Tool](#painting-tool)
- [FOW P2B Bridge](#fow-p2b-bridge)

## Paint 2 Blocking

The `Paint 2 Blocking` plugin is a tool designed for fast gameplay layout iteration. Its primary purpose is to generate 3D `Blockers` from
textures. These textures can be easily modified using the `Paint Mode` provided with the plugin.  

The plugin functions similarly to a classic drawing application, featuring multiple layers that can be shown or hidden. Each layer is drawable
and includes an undo function to cancel modifications.  

This system is highly flexible, allowing users to override the generated `Blockers`. Anything can be spawned from a color shape drawn on the
textures. However, due to texture limitations, unique data cannot be assigned per instance, meaning individual rotations for instanced objects
are not currently supported. This limitation may be addressed in future updates.

## Features

The plugin comes with a few core features, but its ability to be tweaked makes it highly powerful.

### 3D Generation

The plugin extracts `vertices` from a single-color shape on a texture to generate a `Geometry`. The standard approach generates a `Vertex` for
each edge pixel of the shape, which is then simplified using various algorithms.  

Once the geometries are extracted, the 3D generation begins, and `Blockers` are spawned. Their world position is calculated as the average position
of all vertices, and their 3D shape is created by extruding the vertices.  

To improve efficiency, users can spawn an `Actor` that inherits from a `Blocker Interface` instead of generating a standard `Blocker`. These actors
are positioned at the center of the `Vertices` and function the same way. For example, you can create a `Player Start` blocking actor that spawns
based on a specific color, allowing for rapid iteration, even with logical engine elements, when designing a new map.

### Parametric Generation

Generation is controlled using `Data Asset` files. There are two types:

- `Blocker Generation`: is where you will register the colors and bind a `Blockers` to them. You must provide a `Blocker Data` class used during
spawning and specify the corresponding `Blocker` class that reads the data. Each data class has different configurable settings.
- `Template Generation`: Gether a list of `Blocker Generation` data assets and defines which `Blockers` will be generated.

### Custom Blockers

The system is designed to be highly flexible, allowing users to spawn anything with custom settings. Two main classes enable this:

- `Blocker Data`: The default `UP2B_BlockerData` class in the plugin may not include all necessary configuration options. For example, you might need
to adjust lighting settings or introduce custom values for spawned `Blockers`. By overriding this class, you can add any necessary parameters. This
data is constant, meaning all `Blockers` generated from the same color will share the same settings.
- `Blocker`: To correctly read custom data, you must either override `AP2B_Blocker` or implement the `IP2B_Blocker_Interface` when using a custom `Actor`.
These classes function similarly and provide useful methods that are called when a `Blocker` is instantiated. These functions allow you to use the
associated `Blocker Data` to initialize custom settings.

### Painting Tool

You can activate the painting tool at any time in the editor by selecting `Paint 2 Blocking` from the dropdown menu in the top-left corner. This will open
a window similar to Unreal Engine's painting tool but with a custom UI.  

The UI is generated based on the `Data Asset` linked to the selected `Blocker Generator`. Using this tool, you can:
- Generate & delete `Blockers`
- Select preset colors for the paintbrush
- Add new drawing layers  

## FOW P2B Bridge

The `Paint 2 Blocking` plugin is primarily designed to work alongside the `Layered Fog of War` (FOW). Setting up fog custom colliders can be time-consuming,
so a faster system was needed.  

The `FOW P2B Bridge` is a free plugin that depends on both `Paint 2 Blocking` and `FOW`. It provides `Blockers` and `Blocker Data` classes that allow you to
generate collisions, stealth areas, and visual elements from color shapes. The bridge is setup to be used with the MOBA template from the FOW plugin which is
designed for online games.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_