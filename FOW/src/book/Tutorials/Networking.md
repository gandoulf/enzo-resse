# Networking

- [Default replication setup](#default-replication-setup)
- [Manage player team](#manage-player-team)
- [Infinit team](#infinit-team)

> **/!\ This tutorial is made to show how the FOW works with networks, replication knowledge
won't be providen. Networking `GameMode`, `GameState`, `Controller` and `Character` are providen.
You have obsolutly the right to read, copy and use any code you find :) <br />**

This tutorial has been realised in the Tutorial/Maps/TutorialMap_Networking map providen in the
[Demo Project](https://github.com/gandoulf/LayeredFOW_Demo)

# Default replication setup

The `TutorialMap_Networking` has been set up to show you how replication and teams works. To do
so a `BP_TutoralNetworking_GameMode` has been set up with a `BP_TutorialNetworking_PlayerController`
to spawn a `BP_TutorialNetworking_Character` at a `PlayerStart`location depending of the Client team.<br />
To visualize the replication the server will clear the fog of an another spawn point for each team
before the client connection. <br />
* The circle represent the spawn point
* The square is the associated revealed spawn point

![Networking](../../assets/Tutorial/Network/0_NetworkingMapSetup.png)

There is a little trouble with Unreal and singleton instance when they are stored in a static variable.
If you hit the play button with multiple player in the editor, multiple world will be created but inside the
same application, wich means static variable are shared and overriden. To prevent this the FOW is designed to
look for an implementation of `FOW_GetHandlerInstance_Interface` in the `GameState`.<br />

Let's setup the game state. Create a new `My_FOWNetworking_GameState` derived from `GameStateBase`

![Networking](../../assets/Tutorial/Network/1_CreateNewGameState.png)

Open it and go into `ClassSettings` to add the `FOW_GetHandlerInstance_Interface` in the `ImplementedInterfaces`
array.

![Networking](../../assets/Tutorial/Network/2_AddGetHandlerInterface.png)

Now you have to provide the code to the `Find_Level_FOWHandler`.
* Add a `FOW_Handler` variable
* Get the variable and convert it to a `Validate` get, if valide return the variable.
* Else find all actor of class `FOW_Handler`
* If at least one is retruned, set your `FOW_Handler` variable to the first element of the array
* Return the variable

![Networking](../../assets/Tutorial/Network/3_AddCodeToTheInterfaceMethod.png)

Now open the `BP_TutoralNetworking_GameMode` and replace the `GameState` with yours

![Networking](../../assets/Tutorial/Network/4_ChangeDefaultGameState.png)

All set up !
> **Note that if you don't simulate the network in the editor this whole setting
isn't needed, as long as every game instance are separated process you don't need to implemente
the interface.**

Now let's see how the FOW works with replication. First create a new `BP_MyNetworkSettings`
derived from `UFOW_NetworkSettings`.

![Networking](../../assets/Tutorial/Network/5_MakeNetworkSettingClass.png)

Open it and change the `NetworkGameMaxTeamNbr` value from the `Server` to 4. It means
that the `FOW_Handler` will be ready to handle 4 different teams drawing fog seperatly.
(for few reason 4 team with two channels enable is the maximum). Also if you pay attention
the client is set to only one team, which mean that only the client team fog will be updated.<br />
Under those settings you will find check box to allow or not replication and which channel are replicated.
The first channel isn't needed since it represent the fog of what drawers currently see.

![Networking](../../assets/Tutorial/Network/6_SetUpTheLayerSettings.png)

Select the `BP_FOW_Handler`, get into the details panel and change the `NetworkSettingsClass` to
your `BP_MyNetworkSettings`.

![Networking](../../assets/Tutorial/Network/6.1_ChangeFOWHandlerNetworkSettings.png)

Before hitting the play button change the `PlaySettings`. Change the number of players to 4 
and change `NetMode` to `PlayAsListenServer`.

![Networking](../../assets/Tutorial/Network/7_ChangeTheEditorPlaySettings.png)

Now you can hit the play button and see the 4 windows open which your character connecting one by one.
If you do not understand what the fog replication change, go back to your `BP_MyNetworkSettings` and
uncheck `bIsFogStateReplicated`.

![Networking](../../assets/Tutorial/Network/8_NetworkingResult.png)

# Manage player team

The previous part was about to setup the network over the FOW. However you couldn't do anything
regarding which client are associated to which team because of the default system distributing the
players to each team.

Let's see how to do that. Create a `BP_MyFogStateReplication_Server` derived from `AFOW_FogStateReplication_Server`.

![Networking](../../assets/Tutorial/Network/9_CreateNewFogStateReplication.png)

Open it and override the `GetClientTeamIndex` function.

![Networking](../../assets/Tutorial/Network/10_OpenAndOverrideGetClientTeamIndex.png)

Open it. This is where you can manage the client team association. the `PlayerController` is providen,
You should be able to fetch necessary data from your game with it.
For the example let's just do this:
* Get the `NetworkMaxTeamNbr` and substract 1 from it
* Pin the result to a `Radom Integer in Range`
* Pin the result to the return;

![Networking](../../assets/Tutorial/Network/11_AddCustomCodeToGetClientTeamIndex.png)

Now that the server is set up, open your `BP_MyNetworkSettings` and replace the `FogStateReplicationClass`
by your `BP_MyFogStateReplication_Server`.

![Networking](../../assets/Tutorial/Network/12_ChangeFogStateReplicationClassServer.png)

Hit the Play button and see the player beeing associated to a random team !

# Infinit team

In case you want more than 4 team with two channel you can just uncheck `bIsFogStateReplicated`,
Set the `NetworkGameMaxTeamNbr` for both client and server to 1 and provide any team index you
want in the `GetClientTeamIndex` override.

> **This replicated team number issue will be taken care of, it might not allow infinit number but more
than 4 for sure**

![Networking](../../assets/Tutorial/Network/13_InfinitTeamForNonReplicatedFog.png)

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_