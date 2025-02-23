
<p align="center">
  <img src="./assets/icon.png" alt="Greenwich" width="150" height="150" />
</p>

<p align="center">
<i>Join the <a href="https://discord.gg/vfn3NJ3TUm">Discord</a> for support and to chat with people.</i>
</p>

# GreenwichDB
Go back to the start of time, where DataStores weren't complex.

## Installation

Start off by copying [`greenwich.lua`](/greenwich.lua) over to `ServerStorage`. Make sure it's a ModuleScript named `Greenwich`.

If you are using TypeScript with [roblox-ts](https://roblox.ts) - check out [this package](https://npmjs.com/package/@rbxts/greenwichdb)

## Concept

The concept of Greenwich is to provide one DataStore, and just one, in order to completely removes complications. It's faster and lighter on the server, and provides a simple API.

## How does it work?

Simple. We have a `dbFunctions` table and a `greenwich` table. What we do, is define our functions on `dbFunctions`, and then when you call `GetDB`, iterate through each function and return an instance of it. This means that you don't have to type `dbFunctions:Set("hello", "key", "value")` - simply just type `Greenwich:GetDB("hello"):Set("key", "value")` instead.

**TIP**: If you don't like SentenceCase `dbFunctions`, you can use lowercase. For example: `GetDB("hello"):set("key", "value")`

## Usage

To use **Greenwich**, here's a simple showcase down below.

```lua
-- Importing Greenwich:
local ServerStorage = game:GetService("ServerStorage")
local Greenwich = require(ServerStorage:WaitForChild("Greenwich"))

-- Getting a DataStore:
local DB = Greenwich:GetDB("names")

-- Setting data:
DB:Set("noobie", "Absolute gamer")

-- You can use lowercase versions of functions as well:
DB:set("salvage", "Gamer")

-- Getting data:
DB:Get("salvage") -- "Gamer"

-- Check for data:
DB:Has("salvage") -- true

-- Remove data:
DB:Remove("salvage")
```

## Ensure no data is lost

The Greenwich queue is in memory and will die after the game server shutsdown. Put this in a **server script** to ensure no data is lost.

```lua
game:BindToClose(function()
	print("Ending queue..")
	Greenwich:EndQueue()
end)
```