# CLI Installation

### Prerequisites

{% hint style="success" %}
You can avoid this configurational step by using the[ Docker installation process](docker.md).
{% endhint %}

Soketi is based on [uWebSocket.js](https://github.com/uNetworking/uWebSockets.js), a Node.js-based WebSocket server, transpiled from C language.&#x20;

Before installing the CLI version, make sure you have the required dependencies to build soketi:&#x20;

* Python 3.x
* GIT
* The `gcc` compiler and the dependencies for build

### Installing

{% hint style="warning" %}
Due to uWebSocket.js limitations, Soketi does not work on CentOS 7, but it works on CentOS 8. [Check the Github issue](https://github.com/uNetworking/uWebSockets.js/issues/500).
{% endhint %}

The following example works for Ubuntu. For other distributions, consider using the equivalents.

```bash
apt install -y git python3 gcc build-essential
```

### Installing with NPM

{% hint style="info" %}
Node.js LTS (14.x, 16.x, so on) is required due to uWebSockets.js build limitations.
{% endhint %}

soketi may be easily installed via the NPM CLI:

```bash
npm install -g @soketi/soketi
```

After installation, a soketi server using the default configuration may be started using the `start` command:

```
soketi start
```

By default, this will start a server at `127.0.0.1:6001` with the following application credentials:

* App ID: `app-id`
* App Key: `app-key`
* Secret: `app-secret`

The credentials are used to authenticate your frontend and backend applications in order to be able to send messages and receive them in real time.

### What to do next

* [Explore the installation process recommendations below](cli-installation.md#supervisor)
* [Learn how to configure the SSL](../ssl-configuration.md)
* [Learn how to configure the frontend client](../client-configuration/)
* [Learn how to configure the backend](../backend-configuration/)
* [Learn how to customize the applications' credentials for better security](../../app-management/introduction.md)

### Supervisor

To keep the soketi server alive permanently, you should consider [installing](https://www.digitalocean.com/community/tutorials/how-to-install-and-manage-supervisor-on-ubuntu-and-debian-vps) a process manager such as [supervisor](http://supervisord.org), a daemon that can run and restart processes in the background. After installing Supervisor, you may use the following example configuration as a good starting point for launching a soketi server:

```ini
[program:soketi]
process_name=%(program_name)s_%(process_num)02d
command=soketi start
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=ubuntu
numprocs=1
redirect_stderr=true
stdout_logfile=/var/log/soketi-supervisor.log
stopwaitsecs=60
stopsignal=sigint
minfds=10240
```

As you can see in the configuration above, a single soketi server will be started, and this server will auto-restart on failure. Logs will be written to `/var/log/soketi-supervisor.log`.

It's important to note that the `stopwaitsecs` and `stopsignal` configuration options should be set as in the example above. If necessary, you can increase `stopwaitsecs` to a larger value. This is the number of seconds Supervisor will allow soketi to gracefully close all connections when the server is stopping or restarting.

In Linux environments, everything is a file, including active sockets. To track socket connections, soketi is creating file descriptor for each connection. In some cases, you may run into a soft limit on file descriptors set by your operating system. In this situation, you can set the Supervisor `minfds` configuration option to a higher value to allow the operating system to handle more connections.

### Scaling across threads with PM2

Node.js is meant to be ran on one CPU at a given time. This means that multi-threading isn't actually multi-threading in its common sense. To fix this problem, you may use the PM2-ready binary that is shipped with any soketi installation:

```bash
soketi-pm2 start
```

The only remaining caveat is that the processes are like they are horizontally scaled. You may want to configure [horizontal scaling](../../advanced-usage/horizontal-scaling/#cluster-adapter) with the cluster adapter, unless you are also scaling across multiple different instances, in which Redis is the recommended adapter.
