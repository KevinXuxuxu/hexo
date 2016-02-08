title: CChat
date: 2015-09-04 12:45:56
category: "tech"
tags:
---
- A command line tool for chatting.
- Basic P2P & multi chatting is finished. More functions are to be added including
	- better UI (considering `curses`)
	- chatting record export

### Usage

#### Basic commands:

- `name`: set current name to be displayed over conversation. (default `Host`)
- `port`: set current port for establishing host (default `9527`)
- `host`: host a conversation
	1. `waiting for connection`
	-  if anyone connects: `[127.0.0.1:54516] trying to connect`
	- enter `confirm` and start conversation
- `connect`: connect to a given host
	1. `where?` enter ip and port `localhost:9527`
	2. `waiting for acceptance`
	3. `confirmed` and start conversation

#### multi-chatter:
(`main.cpp` in multi-chatter branch)

- `name`, `port` ...
- `info`: print current global variables e.g `name` and `port`
- `host`: start a chat room. Entrance does not require approval.
	- `Bob from [127.0.0.1:54516] joined.`
- `connect`: connect to a given host
	1. `where?` enter ip and port
	2. `waiting for response...`
	3. if succeed, `joined` and start conversation.
