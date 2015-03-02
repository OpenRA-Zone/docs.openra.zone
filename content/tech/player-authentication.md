---
date: 2013-07-01
linktitle: Player authentication
menu:
  main:
    parent: tech
title: Player authentication
description: Player authentication to central and dedicated servers
weight: 90
---

A player must be able to authenticate to the central server. When a player joins a gamelobby at a dedicated server, the dedicated server must be able to verify the player identification with the central server.

# Player registration

++ TODO

# Player login

Login returns Player Authentication Key (PAK), to be used with following requests to DS an CS

# PC->DS authentication (Old idea: hashing and signing)

 - Each dedicated server has a random passphrase assigned to it by the Central Server.
 - Player retrieves public Dedicated Server Passphrase from Central Server
 - Player hashes Player Authentication Key with DS Passphrase
 - Player sends the hashed PAK to DS
 - DS sends hashed PAK to CS
 - CS takes original PAK and hashes also with DS public Passphrase
 - CS compares hashes and returns result

Flaw here is that the DS server OP might replay the players authentication. Are we considering that to be a serious vulnerability at this stage?

# PC->DS authentication (New idea: joincodes)

When a Player client (PC) connects to a Dedicated Server (DS) the client must authenticate to the DS.

 - 1) The Player Client (PC) requests a joincode for a specific Dedicated Server (DS) from the Central Server (CS).
  - The game client displays a 'waiting' screen until the authentication is completed, at normal ping times this should all take under 500ms.
 - 2) The server returns a joincode to the player
  - A joincode is an array of 64 or 128 "random" bytes.
  - The joincode is linked to the playerID and DS ID, and can only be used with the right combination.
  - The joincode is only valid for 30 seconds, this should be more then enough time to join the DS.
 - 3) The player opens a connection to the Dedicated Server and sends playerID` and joincode.
 - 4) The Dedicated Server sends a join validation request (TODO: link) to the Central Server over the open [Tesla](/tech/tesla) connection.
  - This request contains the playerID and the joincode.
  - The dedicated server ID is already known to the server as the open Tesla connection is stateful.
  - The joincode can only be used once
 - 5) The Central Server returns a message with the validation result.
  - When the joincode was valid, the result message also contains the player's details.
 - 6) The Dedicated Server sends a message to the Player Client indicating whether validation succeeded.
  - When the validation failed, the Dedicated Server closes the connection after sending the reject message.
  - When the validation succeeded both parties keep the connection open and can communicate about lobby-related business.

TODO: step 7, let PC indicate to CS that join succeeded. This is required to avoid a rogue DS stealing the PC's joincode and placing a bad score.

TCP hijacking can (should) be avoided by using TLS.

{{%gliffy 7383485 %}}
