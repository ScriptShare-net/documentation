# Core

---

## Server

---

### sharedObject

There is 2 ways to get this object externally but interally you can just use "SS.".

#### Usage 1

```lua
SS = {}
CreateThread(function()
	TriggerEvent('SS:sharedObject', function(obj) SS = obj end)
end)
```

#### Usage 2

```lua
SS = exports["SSCore"]:sharedObject()
```

---

### GetPlayerIdentifiers

This function returns all the players identifiers. The function takes two arguments. The first being the players source and the second is the callback to run once it has collected the identifiers. The function will return a table with the below values:

```
Source - Players source (This changes everytime the players joins the server)
GTA - Players GTA V license (This changes randomly or when the license file is deleted)
Steam - Players Steam license (This sometimes doesn't detect)
Discord - Players Discord license (This only connects if the player has connected discord and FiveM. This should be done the first time the game launches)
Live - Players Microsoft license (Usually only connected when the player has a microsoft account instead of a local user on the computer)
Xbox - Players Xbox license (Only connected if you sign into xbox game pass or xbox video bar)
FiveM - Players FiveM forum license (Only connected if they connect their forum account to FiveM in the main menu)
IP - Players IP address (Changes depending on ISP)
GTA2 - This one happens occasionally for certain people (I have no idea why or what it is but it is orignally license2)
Tokens - This is a table of all the hardware tokens FiveM can find (Some new ones get find randomly)
Identifier - This is the identifier of the player based on the default identifier in the config (Default is discord license)
PermID - This is the unique id generated when someone joins the server (This starts at 1 and keeps going when more people join)
```

#### Usage

```lua
SS.GetPlayerIdentifiers(source, function(identifiers)
	print(json.encode(identifiers))
end)
```

---

### Alert

This function takes a string as its argument and will print the string in console with the `[SSCore]` in front of it. You can also enable or disable alerts in the config so you can quickly turn off or on for debugging. This is on by default.

#### Usage

```lua
SS.Alert("This function works")
```

---

### GetCharacterFromSource

This function gets the character object that is created when a user selects or creates a character. This function takes one argument which is the source of the user.

#### Usage

```lua
local xPlayer = SS.GetCharacterFromSource(source)
```

---

### GetPermIDFromIdentifier

This function gets the PermID from the players identifier. This takes one argument which is the identifier and returns the permid value.

#### Usage

```lua
local PermID = SS.GetPermIDFromIdentifier(identifier)
```

---

### RegisterServerCallback

This function allows you to create a callback on the server that can be called from the client. This takes two arguments being the name of the callback and the callback function.

#### Usage

```lua
SS.RegisterServerCallback("TestCallback", function(cb)
	local xPlayer = SS.GetCharacterFromSource(source)
	cb(xPlayer)
end)
```

---

### Net Events

---

#### Console:Print

Print a string from the client to the server. Used for debugging. Can be disabled in the config.

##### Usage

```lua
TriggerServerEvent("SS:Console:Print", "Print this string")
```

---
