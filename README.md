---
description: Just another simple, fast, and resilient open-source WebSockets server. 📣
---

# 📡 soketi

![](<.gitbook/assets/carbon (22).png>)

The server is built on top of [uWebSockets.js](https://github.com/uNetworking/uWebSockets.js) - a C application ported to Node.js, that claims to be running [_8.5x that of Fastify_](https://alexhultman.medium.com/serving-100k-requests-second-from-a-fanless-raspberry-pi-4-over-ethernet-fdd2c2e05a1e)_ and at least _[_10x that of Socket.IO_](https://medium.com/swlh/100k-secure-websockets-with-raspberry-pi-4-1ba5d2127a23)_. (_[_source_](https://github.com/uNetworking/uWebSockets.js)_)_

soketi implements the [Pusher Protocol v7](https://pusher.com/docs/channels/library\_auth\_reference/pusher-websockets-protocol#version-7-2017-11) - meaning that any Pusher-maintained client can connect to it, bringing a plug-and-play experience for the already-built frontend apps that you already implemented.
