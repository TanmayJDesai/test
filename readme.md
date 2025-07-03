# Development Environment Setup

## Overview

This guide covers setting up the Pulse development environment on Linux (native or WSL2). For WSL2 setup on Windows, see [wsl\_setup.md](wsl_setup.md).

## Repository Setup

In your terminal:

```bash
cd ~
cd home
mkdir -p dev
cd dev
git clone https://gitlab.wa.spectranetix.com/pulse/pulse/-/tree/main?ref\\\_type=heads Pulse
cd Pulse
```

### Troubleshooting

**Repository not Found or Permission Denied problems**

1. Verify that you have access to the repository in GitLab
2. Check the exact repository URL in GitLab
3. Ensure you are using the SSH clone URL (starts with git@)

**SSH Key not being used problem**

1. Test with verbose SSH to see what's going on

```bash
ssh -vT git@gitlab.wa.spectranetix.com
```

## Initialize Git Submodules

```bash
git submodule update --init --recursive
```

Then open in VSCode for development

```bash
code .
```

### Troubleshooting

**Permission denied problem for specific submodules**

1. You need access to additional repositories to initialize these.
2. Contact Kyle or whoever your GitLab admin is and ask them to grant access to:

   * each submodule repository individually
   * the gitlab group/organization containing the submodules (both as developer role)

**Some submodules don't work, others do problem**

1. Test access to specific submodule repositories

```bash
git ls-remote specificsubmodulerepo.git
```

## Docker Development Build

Export the Docker GID:

```bash
export DOCKER\\\_GID=$(getent group docker | cut -d: -f3)
```

Build the development containers:

```bash
docker compose -f docker/docker-compose.yml build
```

## Running with Docker Compose

Start the development environment:

```bash
docker compose -f docker/docker-compose.yml up
```

Use ctrl-c to stop, then run:

```bash
docker compose -f docker/docker-compose.yml down
```

## Python Local Development Environment

Set up the Python virtual environment:

```bash
source scripts/setup-local-env.sh
source env/bin/activate
python3 plugins/pnt/collector.py
source deactivate # To exit the environment
```

## Release Generation and Installation

Generate a release package in the project root (/home/dev/Pulse):

```bash
./scripts/generate-release.sh
```

Then on your target device you should get a tar file (pulse-service-v0.1-beta.tar.gz not pulse-service.tar.gz) untar it:

```bash
tar -xzvf pulse-service-v0.1-beta.tar.gz -C /opt
cd /opt/pulse-service/
```

Then run the installation script:

```bash
./service-install.sh
```

### Troubleshooting Installation

**open /opt/pulse-service/exported-images/\*.tar: no such file or directory problem**

1. This will happen if you do cd /opt/pulse-service because we don't save anything there everything is in the pulse folder in the pulse-service directory.

```bash
cd ..
cd ..
cd home/dev/Pulse
cd pulse-service
./service-install.sh
```

