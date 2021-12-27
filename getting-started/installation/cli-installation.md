# CLI Installation

soketi may be easily installed via the NPM CLI:

```bash
npm install -g @soketi/soketi
```

After installation, a soketi server using the default configuration may be started using the `start` command:

```
soketi start
```

By default, this will start a soketi server at `127.0.0.1:6001` with an application ID of `app-id`, application key of `app-key`, and application secret of `app-secret`.

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

The only remaining caveat is that the processes are like they are horizontally scaled. You may want to configure [horizontal scaling](../../advanced-usage/horizontal-scaling.md#cluster-adapter) with the cluster adapter, unless you are also scaling across multiple different instances, in which Redis is the recommended adapter.