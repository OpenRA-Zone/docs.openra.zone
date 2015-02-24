---
date: 2013-07-01
linktitle: Tesla messages
menu:
  main:
    parent: tech
notoc: notoc
title: Tesla messages
description: Message specifications for the Tesla protocol
weight: 81
---

# Protocol Documentation


## Table of Contents
* [game.proto](#game.proto)
 * [EventGameEnd](#tesla.EventGameEnd)
 * [EventGameStart](#tesla.EventGameStart)
* [lobby.proto](#lobby.proto)
 * [LobbyChatMessage](#tesla.LobbyChatMessage)
 * [LobbyPlayerJoin](#tesla.LobbyPlayerJoin)
 * [LobbyPlayerLeave](#tesla.LobbyPlayerLeave)
 * [LobbyChatMessage.MessageTarget](#tesla.LobbyChatMessage.MessageTarget)
* [players.proto](#players.proto)
 * [PlayerInfo](#tesla.PlayerInfo)
 * [PlayerReference](#tesla.PlayerReference)
 * [PlayerAuthenticationLevel](#tesla.PlayerAuthenticationLevel)
* [validation.proto](#validation.proto)
 * [PlayerJoinRequest](#tesla.PlayerJoinRequest)
 * [PlayerJoinResponse](#tesla.PlayerJoinResponse)
* [Scalar Value Types](#scalar-value-types)



## game.proto


### EventGameEnd


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| GameID | uint64 | required |  |
| EndTime | int64 | required |  |


### EventGameStart


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| GameID | uint64 | required |  |
| StartTime | int64 | required |  |




## lobby.proto


### LobbyChatMessage


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| PlayerID | uint64 | required |  |
| EventTime | int64 | required |  |
| Text | string | required |  |
| Target | LobbyChatMessage.MessageTarget | required |  |


### LobbyPlayerJoin


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| PlayerID | uint64 | required |  |
| EventTime | int64 | required |  |


### LobbyPlayerLeave


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| PlayerID | uint64 | required |  |
| EventTime | int64 | required |  |



### LobbyChatMessage.MessageTarget


| Name | Number | Description |
| ---- | ------ | ----------- |
| All | 1 |  |
| Team | 2 |  |



## players.proto


### PlayerInfo


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| ID | uint64 | required |  |
| DisplayName | string | required |  |


### PlayerReference


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| ID | uint64 | required |  |
| DisplayName | string | required |  |



### PlayerAuthenticationLevel


| Name | Number | Description |
| ---- | ------ | ----------- |
| None | 0 |  |
| Anonymous | 1 |  |
| Member | 2 |  |
| ProMember | 3 |  |
| Mod | 21 |  |
| Admin | 42 |  |



## validation.proto


### PlayerJoinRequest


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| RequestID | uint64 | required |  |
| PlayerID | uint64 | required |  |
| AuthenticationHash | bytes | required |  |


### PlayerJoinResponse


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| RequestID | uint64 | required |  |
| Valid | bool | required |  |




## Scalar Value Types

| .proto Type | Notes | C++ Type | Java Type | Python Type |
| ----------- | ----- | -------- | --------- | ----------- |
| double |  | double | double | float |
| float |  | float | float | float |
| int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int |
| int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long |
| uint32 | Uses variable-length encoding. | uint32 | int | int/long |
| uint64 | Uses variable-length encoding. | uint64 | long | int/long |
| sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int |
| sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long |
| fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int |
| fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long |
| sfixed32 | Always four bytes. | int32 | int | int |
| sfixed64 | Always eight bytes. | int64 | long | int/long |
| bool |  | bool | boolean | boolean |
| string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode |
| bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str |
