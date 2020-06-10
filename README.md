[hub]: https://hub.docker.com/r/onvrb/fivem
[git]: https://github.com/onvrb/fivem

# [onvrb/fivem][hub]

This docker image allows you to run a server for FiveM, a modded GTA multiplayer program.
Upon first run, the configuration is generated in the host mount for the `/config` directory.
The container should be stopped so fivem can be configured to the user requirements in the `/config/cfgs/server.cfg`.

## Licence Key

This image assumes that you give the license key in the configurations, for example in `/config/cfgs/server.cfg`.
A tutorial on how to obtain a licence key can be found [here](https://forum.fivem.net/t/explained-how-to-make-add-a-server-key/56120)

## Usage

docker-compose block:

```sh
version: '3'

services:
  fivem:
    image: onvrb/fivem
    container_name: fivem
    restart: unless-stopped
    stdin_open: true
    tty: true
    volumes:
      - "/home/docker/fivem/roleplay-fivem:/config"
    ports:
      - "30120:30120"
      - "30120:30120/udp"
```

### Environment Varibles

- `RCON_PASSWORD` - A password to use for the RCON functionality of the fxserver. If not specified, a random 16 character password is assigned. This is only used upon creation of the default configs
