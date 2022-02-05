---
description: Soketi is your simple, fast, and resilient open-source WebSockets server. 📣
---

# 📡 soketi

![](<.gitbook/assets/carbon (22).png>)

soketi is your simple, fast, and resilient open-source WebSockets server. 📣

#### Blazing fast speed :zap:

The server is built on top of [uWebSockets.js](https://github.com/uNetworking/uWebSockets.js) - a C application ported to Node.js. uWebSockets.js is demonstrated to perform at levels [_8.5x that of Fastify_](https://alexhultman.medium.com/serving-100k-requests-second-from-a-fanless-raspberry-pi-4-over-ethernet-fdd2c2e05a1e) and at least [_10x that of Socket.IO_](https://medium.com/swlh/100k-secure-websockets-with-raspberry-pi-4-1ba5d2127a23). ([_source_](https://github.com/uNetworking/uWebSockets.js))

#### Cheaper than most competitors 🤑

Compared with Pusher, you can achieve much more for less than one-third of the price.

For a $49 plan on Pusher, you get a limited amount of connections (500) and messages (30M). With Soketi, for the price of an instance on Vultr or DigitalOcean ($5-$10), you get virtually unlimited connections, messages, and some more

Soketi is capable to hold 500 active connections with high traffic on just **1 GB and 1 CPU machines** in the cloud. You can also [get free $100 on Vultr to try out soketi →](https://www.vultr.com/?ref=9032189-8H)

#### Ease of use :baby:

Whether you run your infrastructure in containers or monoliths, soketi got your back. There are multiple ways to [install](getting-started/installation/) and [configure](getting-started/environment-variables.md) soketi, from single instances for development, to tens of active instances at scale with hundreds or thousands of active users.

#### Pusher Protocol v7 :satellite:

soketi implements the [Pusher Protocol v7](https://pusher.com/docs/channels/library\_auth\_reference/pusher-websockets-protocol#version-7-2017-11). Therefore, any Pusher-maintained or compatible client can connect to it, bringing a plug-and-play experience for existing applications that are already compatible with this protocol.

#### App-based access :closed\_lock\_with\_key:

You and your users can access the API and WebSockets through [Pusher-like apps](app-management/introduction.md) which serve keys and secrets to connect or authenticate requests for broadcasting events or checking channels statuses. soketi also comes built-in with support for DynamoDB and SQL-based servers like Postgres.

#### Production-ready! :robot:

In addition to being a good companion during local development, soketi comes with the resiliency and speed required for demanding production applications.

#### Built-in monitoring :chart\_with\_upwards\_trend:

soketi just exposes the metrics to you, you just have to scrape them, whether it's a simple HTTP Client to pull the current usage, or you're using Prometheus to monitor all the connections.
