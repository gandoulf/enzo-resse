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

To understand the technology, you have to see the FOW as a texture:

> **By using a texture, it should be possible to create games with a "flat" map. Gameplay areas
can't be superimposed, or you will discover undesirable parts of it. However, with multiple layers
and by applying transparency, we can get through this problem.**

Quick definition:
A fog of war is a common game mechanic used in strategy and real-time strategy (RTS) games to
simulate uncertainty and limited visibility. It obscures parts of the game map that are not
currently within the player's line of sight or knowledge, typically represented by a shroud or
darkness.

A FOW is just a set of data represented as a texture, which allows the computer to hide some part
of the rendered frame from the player during the post-process pass. It will project the position
of the rendered pixel onto a plane delimiting the FOW. The projection will then query the state
of the fog texture to know if the player has sight on this pixel. It's a simple process of flattening
all the assets onto a plane.

The texture generation is done by elements called "Drawers"; they will compute a texture fragment
of what they see. Drawers can draw any shape to reveal an area. There are two different usages:
- Drawing circles which reveal everything around the player.
- Casting the collision geometry shadow to simulate the sight of the player.

Once every fragment is generated, they will be merged under the fog texture to be rendered.

## Features

### High Definition, Big Map

#### 1. Intro

The Fog of War algorithms are simple in theory but heavy to update. To have a decent frame rate,
you have to downgrade the texture precision to reduce the rasterization time of the drawers, the
texture update on the GPU, or the GPU texture sampling time. The fog update being heavy was also
an obstacle for game development. Maps had to be small for a high fog definition, or the definition
had to be low for huge maps. I've wanted to prevent that and let everyone choose any precision
without any repercussions.

#### 2. Handler, Floor, Tile, Sample

The Fog Of War is split into floors representing parts of your level. You can have as many as you
want, and you can juxtapose or even superpose them to give verticality. Every floor shares the
same settings given from the handler and will have the same precision. They are also divided into
tiles and snapped to a grid to simplify the merge and update process time. The FOW can have up to
8 visibility channels to represent fog. Only 2 channels are used in the given version to represent
3 states of fog:
- Seen: The player came earlier and is aware of the layout of the area.
- Visible: The player directly sees the area.
- Unseen: The player has never seen this area (meaning both of the channels are equal to 0).

It's up to you to find more usages of the 6 other channels. You can also use only one channel to
make MOBA-like games where the map is fully visible.

#### 3. Optimization for Large-Scale Projects

To overcome the update time, the FOW uses samples of fog to send to the GPU and uses binary
compression of everything related to a texture. They are compressed such as 1 bit = 1 pixel. Doing
so reduces the memory usage but also the pixel processing time by doing bitwise operations. Most
of the update work is related to merging two textures, which means applying an "OR" operator between
two textures. Since all the pixels are packed and our computer can use registers up to 512 bits,
the FOW can also compute up to 512 pixels in one operation.

#### 4. Architecture Repercussion

To allow the best usage of binary operation, channels had to be separated and can be seen as N
different textures. Simplified representation of the texture

Normal texture: &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;->&nbsp;&nbsp; FOW texture:<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />
RGBA, RGBA, RGBA &nbsp;&nbsp;->&nbsp;&nbsp; RRR, GGG, BBB, AAA<br />

### Tons of AI

#### 1. Intro

Projects using FOW are mostly games using lots of AI. It was one of the main objectives, being
able to simulate thousands of units drawing fog. This plugin had to be ready for games like
"Among Us" but also for RTS or MOBA like "Age Of Empires" or "League Of Legends." Once more,
performance was the issue and had to be solved without impacting the precision or the map scaling.

#### 2. Drawer, SharedDrawer, Entity, Rasterizer

Each player has a number of units represented in the game. Those units help him to navigate,
discover, and fulfill the objective of the game. To discover the layout of the game, the FOW will
use Drawers. Those drawers are components registered into the FOW, which will generate a fragment
of fog represented as a bit array. This fragment is the representation of the sight of the owning
actor. It can draw any shape and will provide its fragment during the floor update to generate the
Fog Texture. However, merging thousand fragments is really inappropriate. It uses lots of memory,
memory isn't aligned, lots of CPU cache is requested, and it doesn't respect patterns that accelerate
computation. To ameliorate the process, the FOW follows the Data-Oriented Design (DOD) and allows 
developers to use Entities instead of drawers. Entities are the representation of an object in the
game and will provide data to a "SharedDrawer," which will be able to update all registered entities
during a single update.

To generate a fog fragment, every drawer has a reference to a rasterizer. Drawers are data containers
designed to generate geometry that can be given to them. They are simple pieces of code that can be
overridden for specific usage. In the current state, two rasterizers are provided:
- UFOW_R_TriangledGeometryV1, made to draw convex geometry from a set of vertices
- UFOW_R_CircleV1, made to draw a circle from one vertex

#### 3. Optimization for Large-Scale Projects

To fasten the fragment generation process, the FOW packs data and follows DOD architecture.It takes
profit of multithreaded processors by doing asynchronous updates and allows the FOW to make discrete
updates which don't interfere with the game thread. In case of heavy updates, the FOW can be computed
in many Engine frames to prevent game freeze.

The DOD and task system are an entry point to the GPU computation. Everything has been thought to make
it possible and might be developed in the near future.

## Vertical games

### Introduction

It has been a challenge to allow everyone to create vertical top-down games. I took part in the development
of "Alien Dark Descent," and it has been tough to implement ladders and stairs. However, the FOW couldn't
dissociate the bottom from the top. So it was impossible to let the player discover the ground level and
then discover the basement without a level transition. As explained a bit earlier, the Layered FOW is made
out of floors that can be set up anywhere in the game. They will generate fog in the provided area, and
drawers will remove it. Nothing is required from the user to make verticality!

### GPU data transfer

Because of the GPU being the GPU, it was tough to go the simple way and send N textures representing the fog of floors. Plus, the update would have been super heavy. It was necessary to find a workaround to send data of each floor. The problem has been solved by packing floor fog samples into one texture; sample sizes are determined by the intersection of the camera frustum and the floor fog plane. However, a bigger texture will be required to update every floor.

To render correctly superposed floors, the material has to project and find the closest floors to query the fog state.

## Networking

### Introduction

Most of the top-down games we play are competitive or cooperative, which means that the game needs networking.
On that behalf, the FOW has minimal Replication implementation. It's based on the fact that every player runs
the same simulation, which means that every client actor has the same position as the server. If this is
correct, there is no need to replicate the state of the FOG through the network; the only thing to synchronize
is which drawer draws for which team.

### FogStateReplication Client/Server

FogStateReplication is responsible for the synchronization between the client and the server. It's responsible
for fog synchronization; the server is able to send the FOW state to any client for game initialization. And
will provide a team ID to every client. This ID is used in each game instance to enable/disable drawers with the
same ID. Once the state and IDs synchronize, nothing else will go through the network regarding the FOW.

### Replication and Team limitation

To allow FOW state replication, the server has to be aware of the state of each team. It means that a game using 2
channels to represent "Seen" and "Visible" state can only have up to 4 teams. I've talked about it a bit earlier; the
FOW can use at the maximum 8 channels. The replication becomes not only a limitation for games by limiting the
team number, but also a performance limitation. The server user will have to constantly compute the fog of each
team even if only 1 team is displayed. Clients don't have this performance issue since they will update only the
attributed team.

Nevertheless, there is a workaround to palliate this limitation. It's possible to tell the server to compute only
the user team. The network will still work, but the FOW state won't be able to be synchronized in case of late
connection. One more thing to understand is that synchronization is useful only for a certain type of fog. The
client doesn't need any synchronization if the game uses the Visible channel. Once every Drawers will be synchronized
with the correct team, they will remove fog at their location to reproduce the state on the server.

To summarize, you can replicate the FOG state but you will have a team limitation depending on the number of channels
used per team. If you don't enable this replication and let the server compute the fog from its player ID you can
have as much team as you want!

## Developer playground

### Introduction

This part is a bit more personal. I've wanted my plugin to be modular, with replaceable parts. I'm always
thinking that a better version exists which brings the necessity to slice my code and make it overridable.
It even became a pattern for me, making small modules and preventing to the maximum dependencies. On that
behalf, the plugin has many settings variables representing object classes to replace the provided ones.

I'm calling it a playground because it can be really simple modification to test a C++ functionality.
There are lots of modules that are containers where you can try to switch an array for a map, or where
you can add an acceleration structure to help the query function. As an example, I've made a naive collision
system testing collision with every registered collider, but I've also made another one using an AABB tree
to query the colliders in bounds.

### This is Where the Fun Begins!

I'll try to provide everything to let you replace the module and play with the code in the source files.
Here is the list of the modules and their working field:
* UFOW_Rasterizer: You can challenge yourself to find the fastest way to draw a triangle. You can also work on specific rasterizers specific to draw geometry from formulas (Cone, torus, rectangle ...)

* UFOW_CollisionHandler: Key stone of the drawers computation time when casting collision shadow. Accelerate the collider querying with structure (AABB tree, Spatial hashing, octree ...)
* UFOW_OcclusionBuffer: Occlusion system for the CollisionHandler to ignore collider. R&D around the occlusion, the default one use 1D depth buffer
* TFOW_Tile_Base: Merge the drawer fog fragment. You can play with SIMD instruction and find a faster way to merge everything
* UFOW_DrawerComponent: Implement your custom drawer. You can play with tasks and multithreading
* UFOW_SaveLoad: Generate a TArray<uint8> to be written in a file. You can play with pointers and compression
* AFOW_FogStateReplication: If you need to adapt the network to your pipeline 
* AFOW_Handler: If you need to adapt the loading or update pipeline 
* UFOW_Floor: If you need to adapt the update pipeline

## Conclusions

Everything works correctly by default; however, you might need to tweak a few settings and have a good
understanding of how the entities work for games with lots of AI.
You can make extremely vast games without vertical limits.
A simple replication implementation is already done allowing you to make online games.
If you are curious you're more than welcome to replace everything !!!! :)
---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_