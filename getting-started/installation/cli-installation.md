# CLI Installation

Install is done via the NPM CLI:

```bash
npm install -g @soketi/soketi
```

To start the sample server, run:

```
soketi start
```

### Supervisor

To keep the CLI server alive, you might want to use [supervisor](http://supervisord.org), a daemon that can run processes in the background. You can find tons of [tutorials that help you install supervisor,](https://www.digitalocean.com/community/tutorials/how-to-install-and-manage-supervisor-on-ubuntu-and-debian-vps) so we'll focus just on the configuration.

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

As you can see, we run a single process, that will auto-restart on failure and will log to `/var/log/soketi-supervisor.log`.

It's really important to note that `stopwaitsecs` and `stopsignal` should be set like that. Of course, you can increase `stopwaitsecs` to a bigger value, so that when the server is closing, it will give a grace period of `60` seconds to close all sockets.

In Linux, everything is a file. Even active sockets. To track them, soketi is creating file descriptor for each connection. In some cases, you might run into a soft limit, set by your OS, that will keep the file descriptors limit to 1024 or so. In supervisor, you can set `minfds` to a higher value, to let the OS handle more connections.
