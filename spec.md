# Overview
As described [here](purpose.md), Project Red Tie goal is to improve the communication efficiency between the proxy & Minecraft server. In order for it to be done and be optional (as this would require cooperation from both side and be manually enabled) a handshake needs to be integrated.

As for MVP, a plugin message will be used.

# Possible optimizations
Here is a non-exaustive list of what Project Red Tie could improve:
* Skip re-compression when unneeded (e.g. chunk & light packets)
* Better compression algorithm (e.g. zstd instead of zlib)
* Application specific packets converted proxy-side to reduce minecraft load & bandwidth (e.g. more efficient particle effects)

# Handshake
The goal of the handshake is to warn the proxy that all following packets might use a different protocol, and that it needs to comply.

Message should be sent under the channel `redtie:protocol` and might be sent multiple time during a connection lifetime. Value should be presented as JSON:
```json
{
  "headerId": true
}
```
* `headerId`: whether the packet id must be outside of the compressed block or not. Used to skip unnecessary packets.
* TODO

# Protocol changes
| Compressed? | Field name       | Field type | Notes                                          |
|-------------|------------------|------------|------------------------------------------------|
| No          | Packet Length    | VarInt     | Length of all the following                    |
| No          | Packet ID Header | VarInt     | Only if `headerId` is enabled.                 |
| No          | Data Length      | VarInt     | Length of uncompressed (Packet ID + Data) or 0 |
| Yes         | Packet ID        | VarInt     | zlib compressed packet ID                      |
| Yes         | Data             | Byte Array | zlib compressed packet data                    |
