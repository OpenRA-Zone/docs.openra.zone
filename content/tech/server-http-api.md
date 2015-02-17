---
date: 2013-07-01
linktitle: HTTP API
menu:
  main:
    parent: tech
title: HTTP API
description: HTTP API used by game clients and web interface
weight: 70
---

The OpenRa: Zone master server provides an HTTP API to interact with the services.

The API uses named services. Optionaly, GET parameters or POST data are used.

Post and response data are always JSON objects. Acceptable JSOn field and GET parameter values are described using regex. The following regex syntax is used: https://code.google.com/p/re2/wiki/Syntax

# Accounts
The ORAZ API provides several API services concerning Accounts

## Register `POST /accounts/register`
Register a new account.

Post data:

 - {{%jsonfield displayname string "[a-zA-Z0-9 ]{3,30}" "The wanted display name." %}}
 - {{%jsonfield username string "[a-zA-Z0-9 \-]{6,30}" "The wanted username." %}}
 - {{%jsonfield password string "(base64 88 chars)" "The base64 encoded sha512 hash of the player's password." %}}
 - {{%jsonfield email string "(TODO@TODO.TODO)" "The player's email address." %}}

Response data:

 - {{%jsonfield success boolean "" "When true: the registration was successfull." %}}
 - {{%jsonfield error string "" "Error string. When `success` is `false` it is set to one of the following values:" %}}
  - `invalid displayname`
  - `invalid username`
  - `invalid password`
  - `invalid email`
  - `displayname taken`
  - `username taken`
  - `email used`

This service can be called with only a username or displayname to just check if the username or displayname is free.

## Authenticate `POST /accounts/authenticate`
Authenticate an account. This service returns an authentication token.
Authentication tokens are removed when not used for over 7 hours, unless the token was requested to be permanent ("remember this computer").

Post data:

 - {{%jsonfield username string "" "The players username" %}}
 - {{%jsonfield password string "base64 88 chars" "The base64 encoded sha512 hash of the player's password." %}}
 - {{%jsonfield permanent bool "" "When true, the requested authentication token should be valid permanently." %}}


Response data:

 - {{%jsonfield success boolean "" "" %}}
 - {{%jsonfield error string "" "Error value. Set to the following error value when `success` is `false`:" %}}
  - {{%jsonfield wrong userpass "" "We don't disclose which of the two was wrong for security reasons." %}}
 - {{%jsonfield token string "" "Authentication token, only filled when field `success` is `true`." %}}


