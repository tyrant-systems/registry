# Registry

* * *

## About

_A self-hosted, private container image registry._

## Usage

### Prelude

- An existing domain
- A running `docker swarm` with at least one node and a `swarm` network
- A set of certificates that are externally managed

### Deploy

- Create expected directories and files:
```
./bin/bootstrap.sh
```
- Create the directory `/mnt/registry`
- Update `./local/config.env` with deployment specific values
- Update `./local/htpasswd` with `$user:$password` in the proper format and syntax
- Copy certificates into `./local/certs`
- Ensure *at least one* node is tagged with `registry=true`, e.g.:
```
docker node update --label-add registry=true ${NODE_ID|NODE_NAME}
```
- Run:
```
docker stack deploy -c stack.yml registry
```
- From a browser, test the service by navigating to:
```
https://domain.co/v2/_catalog
```

### Management

This repository contains a script for interacting with the registry. It's essentially
a thin client wrapper that invokes `curl` commands against the `v2` registry API.

Client configuration resides under `~/.registry.rc/config`.
