---
date: 2013-07-01
linktitle: Tesla protocol
menu:
  main:
    parent: tech
title: Tesla protocol
description: Communication protocols between dedicated server and central server
weight: 80
aliases:
    - /tech/ds-cs-communication/
---

This document describes how the Dedicated Server (DS) and Central Server (CS) comunicate.

The DS opens a TCP connection to the CS. Data in messages between the DS and CS are encoded with protobuf. Because protobuf does not provide a data encapsulation format for tcp, the messages on the TCP connection are encapsulated in a custom binary format.

# Encoding

Data encoding is achieved with protobuf.

> "Protocol buffers are Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data – think XML, but smaller, faster, and simpler. You define how you want your data to be structured once, then you can use special generated source code to easily write and read your structured data to and from a variety of data streams and using a variety of languages – Java, C++, or Python."

Protobuf structure definitions are created for the different message types that can be sent

## List of data structures

 - A
 - B
 - TODO

# Encapsulation

The encoded data is sent in a custom envelope following a simple scheme:

 - 2 bytes uint16: message type (event code)
 - 4 bytes data length (n)
 - n bytes data

The hard limit for a single message is: 6+(2^32) bytes (~4.3GB). (A softlimit should be used to avoid ddos attacks. The value of the soft limit can be decided after implementation.)


## Security & TLS
The initial protocol will not use TLS. The information transmitted over the TCP connections won't contain 

## Message type
The message type indicates which type of data is encoded. In most cases this will also indicate the event for which the data was sent.

 - Player join
 - Player leave
 - Chat message
 - etc.

Each of these types relates to a protobuf structure definition which can be used to decode the data.

# Protocol magic
When the DS opens a new connection to the CS, at first a 4-byte protocol magic value is sent to identify that the incomming connection is (probably) a valid ORAZ DS<->CS connection. It's not a 100% foolproof method, but helps in filtering away most erroneous connections.

# Sequence

TODO: sequence of messages between DS and CS
