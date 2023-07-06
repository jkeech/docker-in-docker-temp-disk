# Running docker-in-docker from a temp disk
Example of Codespaces running docker-in-docker from the temp disk

## How it works
The devcontainer  (`.devcontainer/devcontainer.json`) is a minimal Ubuntu 22.04 image with the `docker-in-docker` feature added in. In the `Dockerfile`, docker's `/etc/docker/daemon.json` is configured to set the `data-root` to be `/tmp/docker` so that the daemon uses `/tmp/docker` instead of `/var/lib/docker` for images/containers/etc.

In Codespaces, the `/tmp` folder is bind-mounted to a local-attached SSD which has higher IOPS and throughput than the persistent volume, but the tradeoff is that it's ephemeral and gets wiped on restarts. For this sample repo, that means every time you restart your codespace, the docker images and containers start from a clean slate and do not persist.