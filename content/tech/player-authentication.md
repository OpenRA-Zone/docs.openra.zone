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

# Identification towards dedicated server

 - Each dedicated server has a random passphrase assigned to it by the Central Server.
 - Player retrieves public Dedicated Server Passphrase from Central Server
 - Player hashes Player Authentication Key with DS Passphrase
 - Player sends the hashed PAK to DS
 - DS sends hashed PAK to CS
 - CS takes original PAK and hashes also with DS public Passphrase
 - CS compares hashes and returns result

Flaw here is that the DS server OP might replay the players authentication. Are we considering that to be a serious vulnerability at this stage?
