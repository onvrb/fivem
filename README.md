[hub]: https://hub.docker.com/r/onvrb/fivem
[git]: https://github.com/onvrb/fivem

[![Docker Pulls](https://img.shields.io/docker/pulls/onvrb/fivem.svg)][hub]

# [onvrb/fivem][hub]

This is an **advanced** implementation of a docker image that allows you to run a server for [FiveM](https://fivem.net/) through [txAdmin](https://github.com/tabarra/txAdmin) web panel.

Upon first run, the configuration is generated in the host mount for the `/config` directory.
The container should be stopped so fivem can be configured to the user requirements in the `/config/cfgs/server.cfg`.

**This image will not start the server!** You still need to access txAdmin on the port 40120 to start the server, specially on the initial configuration.

## Access

The ports listened are 30120 (FiveM) and 40120 (txAdmin), however only 30120 is exposed to the host so players can connect. Port 40120 can be accessed by other containers, like [letsencrypt](https://hub.docker.com/r/linuxserver/letsencrypt) for reverse-proxy or locally on http://localhost:40120 after exposing the port. I do not recommend exposing port 40120 to the host if you don't know what you're doing.

## Licence Key

This image assumes that you give the license key in the configurations, for example in `/config/cfgs/server.cfg`.
A tutorial on how to obtain a licence key can be found [here](https://forum.fivem.net/t/explained-how-to-make-add-a-server-key/56120)

## Docker Compose

```yml
version: '3'

services:
  fivem:
    image: onvrb/fivem
    container_name: fivem
    restart: unless-stopped
    stdin_open: true
    tty: true
    volumes:
      - "/path/to/config:/config"
    ports:
      - "30120:30120"
      - "30120:30120/udp"
      #- "40120:40120" #expose txAdmin to host
```

### Other Environment Varibles

- `RCON_PASSWORD` - A password to use for the RCON functionality of the FXserver. If not specified, a random 16 character password is assigned. This is only used upon creation of the default configs
