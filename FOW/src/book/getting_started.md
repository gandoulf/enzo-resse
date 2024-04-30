# Getting Started

## Table of Contents

- [The Fog Of War is Only a Texture](#the-fog-of-war-is-only-a-texture)
- [Features](#features)
  - [High Definition, Big Map](#high-definition-big-map)
  - [Tons of AI](#tons-of-ai)
  - [Vertical Games](#vertical-games)
  - [Networking](#networking)
  - [Developer Playground](#developer-playground)
  - [Conclusions](#conclusions)

## The Fog Of War is Only a Texture

Understanding the technology requires seeing the Fog of War (FOW) as a texture:

> **By utilizing a texture, it should be possible to create games with a "flat" map. Gameplay areas cannot be superimposed,
or undesirable parts of it will be revealed. However, by employing multiple layers and applying transparency, this issue 
can be addressed.**

Quick definition:
The fog of war is a common game mechanic used in strategy and real-time strategy (RTS) games to simulate uncertainty and
limited visibility. It obscures parts of the game map that are not currently within the player's line of sight or knowledge,
typically represented by a shroud or darkness.

FOW is merely a set of data represented as a texture, allowing the computer to conceal some parts of the rendered frame from
the player during the post-process pass. It will project the position of the rendered pixel onto a plane delimiting the FOW.
The projection will then query the state of the fog texture to determine if the player has sight on this pixel. It's a simple
process of flattening all the assets onto a plane.

The texture generation is carried out by elements called "Drawers"; they compute a texture fragment of what they see. Drawers
can draw any shape to reveal an area, with two primary usages: drawing circles to reveal everything around the player and casting
the collision geometry shadow to simulate the player's sight.

Once every fragment is generated, they are merged under the fog texture to be rendered.

## Features

### High Definition, Big Map

#### 1. Introduction

The Fog of War algorithms are simple in theory but resource-intensive to update. To maintain a decent frame rate, texture
precision needs to be downgraded to reduce rasterization time of the drawers, texture update time on the GPU, or GPU texture
sampling time. The heavy fog update also posed obstacles for game development. Maps had to be small for high fog definition,
or the definition had to be low for huge maps. I've aimed to prevent this and allow everyone to choose any precision without
repercussions.

#### 2. Handler, Floor, Tile, Sample

The Fog Of War is divided into floors representing parts of your level. You can have as many as you want, and they can be
juxtaposed or even superposed to add verticality. Every floor shares the same settings provided by the handler and will have
the same precision. They are also divided into tiles and snapped to a grid to simplify the merge and update process. The FOW
can have up to 8 visibility channels to represent fog, but only 2 channels are used in the given version to represent 3 states
of fog:
- Seen: The player has visited the area and is aware of its layout.
- Visible: The player directly sees the area.
- Unseen: The player has never seen this area (meaning both channels are equal to 0).

It's up to you to find more uses for the other 6 channels. You can also use only one channel to create MOBA-like games where
the map is fully visible.

#### 3. Optimization for Large-Scale Projects

To overcome update time, the FOW uses fog samples sent to the GPU and binary compression of everything related to a texture.
They are compressed such that 1 bit equals 1 pixel. This reduces memory usage and pixel processing time through bitwise operations.
Most of the update work involves merging two textures, applying an "OR" operator between them. Since all pixels are packed and
computers can use registers up to 512 bits, the FOW can compute up to 512 pixels in one operation.

#### 4. Architecture Repercussions

To allow the best usage of binary operations, channels had to be separated and can be seen as N different textures. Simplified
representation of the texture:

Normal texture: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;->&nbsp;&nbsp; FOW texture:<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />


### Tons of AI

#### 1. Introduction

Projects utilizing FOW primarily involve games with extensive AI usage. One of the primary objectives was to simulate thousands
of units drawing fog. This plugin needed to be adaptable for games like "Among Us" as well as for RTS or MOBA games like "Age Of Empires"
or "League Of Legends." Once again, performance was a concern and needed to be addressed without compromising precision or map scaling.

#### 2. Drawer, SharedDrawer, Entity, Rasterizer

Each player controls a number of units within the game, aiding in navigation, exploration, and achieving game objectives. To explore
the game's layout, the FOW employs Drawers. These drawers are components registered within the FOW, generating fog fragments represented
as bit arrays. These fragments depict the sight of the owning actor, capable of drawing any shape and providing its fragment during
floor updates to generate the Fog Texture. However, merging thousands of fragments is inefficient, consuming excessive memory, lacking
alignment, demanding significant CPU cache, and failing to adhere to patterns that accelerate computation. To improve this process,
the FOW follows Data-Oriented Design (DOD) principles and enables developers to utilize Entities instead of drawers. Entities represent
objects in the game and supply data to a "SharedDrawer," which updates all registered entities during a single update.

To generate a fog fragment, each drawer has a reference to a rasterizer. Drawers serve as data containers designed to generate geometry
provided to them. They are simple code components that can be overridden for specific purposes. Currently, two rasterizers are available:
- UFOW_R_TriangledGeometryV1: Draws convex geometry from a set of vertices
- UFOW_R_CircleV1: Draws a circle from a single vertex

#### 3. Optimization for Large-Scale Projects

To expedite fragment generation, the FOW packs data and adheres to DOD architecture. It utilizes multithreaded processors through
asynchronous updates, allowing discrete updates that do not interfere with the game thread. In cases of heavy updates, the FOW can be
computed across multiple engine frames to prevent game freezing.

The DOD and task system serve as entry points to GPU computation. Every effort has been made to facilitate this and may be further
developed in the future.

### Vertical Games

#### Introduction

Enabling the creation of vertical top-down games for everyone has been a challenge. I participated in the development of "Alien Dark Descent,"
where implementing ladders and stairs proved difficult. However, the Fog of War (FOW) couldn't distinguish between the bottom and the top,
making it impossible to allow players to explore the ground level and then the basement without a level transition. As mentioned earlier,
the Layered FOW comprises floors that can be placed anywhere in the game. They generate fog in the designated area, which drawers subsequently
remove. No additional user input is necessary to introduce verticality!

#### GPU Data Transfer

Due to the GPU's limitations, it was challenging to send N textures representing the fog of floors. Additionally, the update process would
have been overly burdensome. It was necessary to devise a method to transmit data for each floor. This issue was addressed by packing floor
fog samples into one texture, with sample sizes determined by the intersection of the camera frustum and the floor fog plane. However, updating
every floor will require a larger texture.

To correctly render superposed floors, the material must project and identify the closest floors to query the fog state.

### Networking

#### Introduction

Most top-down games we play are competitive or cooperative, necessitating networking. In this regard, the FOW features minimal Replication
implementation. It operates on the premise that every player runs the same simulation, meaning every client actor shares the same position as
the server. If this condition holds true, there is no need to replicate the FOG state over the network; the only synchronization required is
determining which drawer represents which team.

#### FogStateReplication Client/Server

FogStateReplication facilitates synchronization between the client and the server. It manages fog synchronization; the server can send the
FOW state to any client for game initialization and assigns a team ID to each client. This ID is utilized in each game instance to enable/disable
drawers associated with the same ID. Once the state and IDs are synchronized, no further FOW-related data is transmitted over the network.

#### Replication and Team Limitation

To enable FOW state replication, the server must be aware of the state of each team. This means that a game using 2 channels to represent
"Seen" and "Visible" states can only accommodate up to 4 teams. As discussed earlier, the FOW can utilize a maximum of 8 channels. Replication
not only limits the number of teams a game can have but also imposes performance constraints. The server user must continuously compute
the fog for each team, even if only 1 team is displayed. Clients do not encounter this performance issue as they only update the attributed
team.

However, there is a workaround to mitigate this limitation. The server can be instructed to compute only for the user's team. While the
network will still function, FOW state synchronization will not be possible in case of a late connection. It's important to note that
synchronization is only necessary for a specific type of fog. Clients do not require synchronization if the game employs the Visible channel.
Once all drawers are synchronized with the correct team, they will remove fog at their location to replicate the server's state.

In summary, FOG state replication is possible but limited by the number of channels used per team. Alternatively, allowing the server to
compute the fog based on the player's ID removes this limitation, enabling as many teams as desired!

### Developer Playground

#### Introduction

This section is somewhat personal. I aimed for my plugin to be modular, with interchangeable parts. I've always believed that a better
version exists, leading me to segment my code and make it replaceable. This approach has become a pattern for me, creating small modules
and minimizing dependencies. Accordingly, the plugin includes numerous settings variables representing object classes to replace the
provided ones.

I call it a playground because it allows for simple modifications to test C++ functionality. There are numerous modules that serve as
containers for experimentation, enabling users to swap arrays for maps or add acceleration structures to aid in query functions. For
example, I've created a naive collision system that tests collisions with every registered collider, as well as another using an AABB
tree for querying colliders within bounds.

#### This is Where the Fun Begins!

I aim to provide everything necessary for users to replace modules and experiment with the code in the source files. Here is a list
of the modules and their intended use:

- UFOW_Rasterizer: Experiment with the fastest way to draw a triangle or develop rasterizers specific to drawing geometry from formulas (e.g., Cone, torus, rectangle...)
- UFOW_CollisionHandler: Crucial for drawer computation time when casting collision shadows. Accelerate collider querying with structures (e.g., AABB tree, Spatial hashing, octree...)
- UFOW_OcclusionBuffer: Implements an occlusion system for the CollisionHandler to ignore colliders. Research and development around occlusion, with the default using a 1D depth buffer.
- TFOW_Tile_Base: Merges drawer fog fragments. Experiment with SIMD instructions and find a faster way to merge everything.
- UFOW_DrawerComponent: Implement custom drawers. Experiment with tasks and multithreading.
- UFOW_SaveLoad: Generates a TArray<uint8> to be written in a file. Experiment with pointers and compression.
- AFOW_FogStateReplication: Adapt the network to your pipeline.
- AFOW_Handler: Adapt the loading or update pipeline.
- UFOW_Floor: Adapt the update pipeline.

### Conclusions

Everything functions correctly by default, but users may need to adjust some settings and have a good understanding of how entities
work for games with extensive AI usage. Vast games without vertical limits can be created, and a simple replication implementation
allows for the creation of online games. Curious users are encouraged to replace everything and experiment!

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_