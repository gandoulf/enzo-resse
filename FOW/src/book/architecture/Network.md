# Network

## Table of contents

- [Explanation](#explanation)
	- [Network Settings](#network-settings)
	- [Fog State Replication](#fog-state-replication)
		- [Server](#server)
		- [Client](#client)
- [Conclusion](#conclusion)

## Explanation

The `Layered Fog of War` is ready for online games but requires a good understanding of the `replication` provided by Unreal,
and how the `LFOW` uses it. To begin with, the `Fog State` isn't replicated; it can be synchronized to the client, but the
`LFOW` will never continually send fog data over the network.

The `LFOW` relies on the `simulation`, ensuring the state of the `server` and the `client` remains the same as long as the
position of the drawer is replicated and correctly updated. In case of latency or client disconnection, the `LFOW` server can,
as mentioned earlier, synchronize and send the fog state through `RPC` to the `clients`.

The plugin includes the concept of `teams`, which can be seen as data duplication. If the `LFOW` is set up with 2 channels and
3 teams, it will use 6 channels internally. Currently, it can only manage up to 8 channels, which means a maximum of 4 teams
with 2 channels each.

However, many games don't need to synchronize the `Fog State` and rely only on the `simulation`. MOBA games like `League of
Legends` or `Dota` will only use a single channel to represent what is currently visible. For games using such a setup, the
team limit disappears.

### Network Settings

The `UFOW_NetworkSettings` class is designed to override the `FOWHandler` variables for online games and set up different
behaviors depending on the `Net Status`. `Server`, `Client`, and `Spectators` require more or less data to be computed by the
`LFOW`. For example, a `Client` only needs to compute the state of its team since it should never see what the opponent sees.
However, the `Server` needs to store the state of each team in case of client re-synchronization.

### Fog State Replication

`AFOW_FogStateReplication` is the base class for every `Online` game instance implementing the `LFOW`. The server will have
its own class and will spawn a new one for every client. It will manage the network used by the plugin, handle connection and
disconnection, and provide useful `RPC` to synchronize every game instance. For now, it will only attribute a `player ID` to
every client which is `replicated` and provide methods to synchronize the Fog through `RPC` if needed.

#### Server

`AFOW_FogStateReplication_Server`

#### Client

`AFOW_FogStateReplication_Client`

## Conclusion

The `LFOW` plugin replication implementation is very lightweight and doesn't provide much assistance for the development of
online games. The main reason for this light implementation is to avoid overloading the bandwidth and to prevent forcing its
use, as many games like `RTS` use `simulation` to avoid the `replication` of thousands of units. This means that developers will
need to implement events themselves to control the status of the `Components` and `Entities`.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_