---
description: "pWS is a free, open-source alternative for the Pusher service. \U0001F4E1"
---

# 📡 Meet pWS

![](.gitbook/assets/carbon-20-.png)

pWS is a free, open-source Pusher drop-in alternative. 📡

The server is built on top of [uWebSockets.js](https://github.com/uNetworking/uWebSockets.js) - a C application ported to Node.js, that claims to be running [_8.5x that of Fastify_](https://alexhultman.medium.com/serving-100k-requests-second-from-a-fanless-raspberry-pi-4-over-ethernet-fdd2c2e05a1e) _and at least_ [_10x that of Socket.IO_](https://medium.com/swlh/100k-secure-websockets-with-raspberry-pi-4-1ba5d2127a23)_. \(_[_source_](https://github.com/uNetworking/uWebSockets.js)_\)_

The difference between pWS and Socket.IO is in terms of speed. pWS is supported by Pusher-maintained clients, bringing portability and plug-and-play functionality with already frontend apps that already use Pusher clients.

The server is entirely compatible with the [Pusher Protocol v7](https://pusher.com/docs/channels/library_auth_reference/pusher-websockets-protocol#version-7-2017-11) and tries to keep up with the [HTTP REST API reference](https://pusher.com/docs/channels/library_auth_reference/rest-api/) as fast as possible.

