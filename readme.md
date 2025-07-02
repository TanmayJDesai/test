# Development Environment Setup

## Overview

This guide covers setting up the Pulse development environment on Linux (native or WSL2). For WSL2 setup on Windows, see [wsl_setup.md](wsl_setup.md).

## Repository Setup

In your terminal:

```
cd ~
cd home
mkdir -p dev
cd dev
git clone https://gitlab.wa.spectranetix.com/pulse/pulse/-/tree/main?ref_type=heads Pulse
cd Pulse
```

### Troubleshooting

**Repository not Found or Permission Denied problems**

1. Verify that you have access to the repository in GitLab
2. Check the exact repository URL in GitLab
3. Ensure you are using the SSH clone URL (starts with git@)

**SSH Key not being used problem**

1. Test with verbose SSH to see what's going on

```
ssh -vT git@gitlab.wa.spectranetix.com
```

## Initialize Git Submodules

```
git submodule update --init --recursive
```

Then open in VSCode for development

```
code .
```

### Troubleshooting

**Permission denied problem for specific submodules**

1. You need access to additional repositories to initialize these.
2. Contact Kyle or whoever your GitLab admin is and ask them to grant access to:
   - each submodule repository individually
   - the gitlab group/organization containing the submodules (both as developer role)

**Some submodules don't work, others do problem**

1. Test access to specific submodule repositories

```
git ls-remote specificsubmodulerepo.git
```

## Docker Development Build

Export the Docker GID:

```
export DOCKER_GID=$(getent group docker | cut -d: -f3)
```

Build the development containers:

```
docker compose -f docker/docker-compose.yml build
```

## Running with Docker Compose

Start the development environment:

```
docker compose -f docker/docker-compose.yml up
```

Use ctrl-c to stop, then run:

```
docker compose -f docker/docker-compose.yml down
```

## Python Local Development Environment

Set up the Python virtual environment:

```
source scripts/setup-local-env.sh
source env/bin/activate
python3 plugins/pnt/collector.py
source deactivate
```

### Troubleshooting Python Setup

You will get a big error when running the first command 'source scripts/setup-local-env.sh'

```
bash: env/bin/activate: No such file or directory
Installing Python dependencies...
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try apt install
    python3-xyz, where xyz is the package you are trying to
    install.
 
    If you wish to install a non-Debian-packaged Python package,
    create a virtual environment using python3 -m venv path/to/venv.
    Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
    sure you have python3-full installed.
 
    If you wish to install a non-Debian packaged Python application,
    it may be easiest to use pipx install xyz, which will manage a
    virtual environment for you. Make sure you have pipx installed.
 
    See /usr/share/doc/python3.12/README.venv for more information....
```

This occurs because you don't have python virtual environment support installed and the virtual env isn't setup properly. Follow the steps below to fix:

```
sudo apt install python3.12-venv -y
python3 -m venv pulse-env
```

Make sure the environment was created:

```
ls -la pulse-env/
```

Activate the environment:

```
source pulse-env/bin/activate
```

Install all the requirements:

```
pip install -r requirements.txt
```

Run the setup script:

```
source scripts/setup-local-env.sh
```

## Release Generation and Installation

Generate a release package in the project root (/home/dev/Pulse):

```
./scripts/generate-release.sh
```

Then on your target device you should get a tar file (pulse-service-v0.1-beta.tar.gz not pulse-service.tar.gz) untar it:

```
tar -xzvf pulse-service-v0.1-beta.tar.gz -C /opt
cd /opt/pulse-service/
```

Then run the installation script:

```
./service-install.sh
```

### Troubleshooting Installation

**open /opt/pulse-service/exported-images/*.tar: no such file or directory problem**

1. This will happen if you do cd /opt/pulse-service because we don't save anything there everything is in the pulse folder in the pulse-service directory.

```
cd ..
cd ..
cd home/dev/Pulse
cd pulse-service
./service-install.sh
```
