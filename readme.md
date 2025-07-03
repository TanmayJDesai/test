
# Integration Quirks and Development Tips

## Overview

This document covers integration notes and quirks with the Pulse tooling that have popped up as part of this tooling's development.

## mDNS Discovery

Most services that Pulse is interested in publish themselves over mDNS so as to more easily discover devices of a particular type.
For instance, VICTORY announcement strings over Zeroconf appear as `_vic-mgt._tcp.local.`, while SOSA services use `_sosa-mgt._tcp.local.`.
Announcement strings can also have substrings which more accurately describe the service, be it `_sys-mgr._sub.` for System Manager or `_pic._sub.` for Plug-In Cards.

### Quirks

During integration with the chassis, it was noted that VICTORY services will quickly respond with the host platform's Zeroconf targets, but will take a more significant amount of time to publish their other interfaces.
For example, say the PNT card has the following 3 interfaces that it's using for its services: `eth0`, `eth1`, and `eth2`.

* When running on the SBC, the PNT service's Zeroconf utility published their endpoint address as that specific to `eth1`.
* The subsequent publication of the other interfaces didn't come till 20-30 seconds later.

All this to say, it's beneficial to be generous with the times for the mDNS environment variables, specifically the "MDNS_SETTLE_DELAY". This allows the plugin to listen for a decent amount of time (say 30 seconds) before it determines that it's found as many devices as it could.
Unsure as to why the discovery decides to delay those ethernet interfaces until significantly later on, but they do appear consistently afterwards.

## Docker Installation Issues

There have been issues when performing a second installation with the `service-install.sh` script. If the device has already had its Telegraf docker image loaded, loading the second image after having run the first may result in some odd behavior - specifically, if running with the newer image, it may think that certain buckets already exist.

### Solution

When running the `service-install.sh` a second time on the same device, be sure to run a `docker container prune` and `docker image prune` prior to installing (or after running - the services will need to be stopped before cleaning up the docker space). This can be done by running `systemctl stop pulse.service`.
After the dangling images and stopped containers have been cleaned up the leftover buckets should no longer throw any errors.

## Docker Container Conflicts

**✘ Container influxdb    Error response from daemon: Conflict. The cont... problem**

This basically just means there are already instances of these containers (if you just clear influxdb, Grafana and telegraf will still throw an error so follow the instructions below):

```
docker compose -f docker/docker-compose.yml down
docker container prune -f
docker rm -f influxdb grafana telegraf-collector
export DOCKER_GID=$(getent group docker | cut -d: -f3)
docker compose -f docker/docker-compose.yml up
```

Then you can access the influxdb to start querying at localhost:8086
The username and password can be found in docker/secrets directory

## Docker WSL2 Integration Issues

**Docker not part of WSL2 instance or docker errors**

1. Can typically be solved by going to docker desktop
2. Settings --> General --> "Use the WSL 2 based engine" --> Apply and Restart
3. Settings --> Resources --> WSL Integration --> Make sure both Ubuntu and Enable integration with my default WSL distro are selected --> Apply and Restart

**Python Environment Issues**

**SecurityError when running the activate scripts function**

This happens because of some permission issues.

For detailed Python setup instructions, see [python_setup.md](python_setup.md).
