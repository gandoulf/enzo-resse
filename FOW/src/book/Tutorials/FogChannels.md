# Fog Channels

- [Basic](#basic)
- [Advanced](#advanced)

This tutorial is based on solo game, every things related to channels need to be taken with cautious
when applied to teams. However everythings works the same, teams will only limite the number of 
availlable channels.

## Basic

The FOW has up to 8 configurable channels that you can use.(Be carefull with game having teams)
The channels may or may not be all used, for the default setup of the FOW only two channels are
used:
* First channel define what the player currently see.
* Second channel define what the player has seen;

This set up is mostly used for narative game or RTS with procedural maps but you might want to make
a game more MOBA oriented with everything reveald to the players, which means that you only need the
first channel to represent the sight of the player.

Let's change the FOW to have only one channel. First select the `BP_FOW_Handler` get to details panel
and click on the `FOWFloorTilesClass` input field and select `TFOW_T128b_1Chan_Pck_Class`.

![Fog channels](../../assets/Tutorial/FogChannel/1_ChangeTileFormat.png)

Still in the `BP_FOW_Handler` details panel, find the `FOWShaderClass` variable and open the providen
material, it should be `MPP_FOW_Floors`.

![Fog channels](../../assets/Tutorial/FogChannel/2_OpenTheFOWMaterial.png)

Find the material function with 8 channel output pin and unlink the `chan2` from the linked `lerp` node.
The `Alpha` value should be set to 1.

![Fog channels](../../assets/Tutorial/FogChannel/3_UnpinBlackChannelSetAlphaTo1.png)

You should be done, press play and check that the FOW correctly display only one channel.

![Fog channels](../../assets/Tutorial/FogChannel/4_GameWithOnlyOneChannelComputed.png)

You might have figured out that only doing the material part would have do the tricks and yes it would
have. But you would have let the FOW doing all the computation in CPU and GPU of the `Chan2`.

## Advanced

In the advanced part I'll show you how to implement and use more than 2 channels by creating new `FOW_Tile_Class`
and `FOW_LayerSetting`. To be done ...

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_