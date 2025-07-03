# Python Local Development Environment Setup

## Overview

This guide covers setting up the Python development environment for Pulse. The default setup script can be troublesome, so this document provides a step-by-step approach to get your Python environment working correctly.

## Initial Setup Attempt

First, try the standard setup process:

```
source scripts/setup-local-env.sh
source env/bin/activate
python3 plugins/pnt/collector.py
source deactivate
```

## Troubleshooting Common Python Setup Issues

You will likely get a big error when running the first command 'source scripts/setup-local-env.sh'

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

## Manual Virtual Environment Setup

This occurs because you don't have python virtual environment support installed and the virtual env isn't setup properly. Follow the steps below to fix:

### Install Python Virtual Environment Support

```
sudo apt install python3.12-venv -y
```

### Create Virtual Environment

```
python3 -m venv pulse-env
```

### Verify Environment Creation

Make sure the environment was created:

```
ls -la pulse-env/
```

### Activate the Environment

```
source pulse-env/bin/activate
```

### Install Requirements

Install all the requirements:

```
pip install -r requirements.txt
```

### Run Setup Script

Now run the setup script:

```
source scripts/setup-local-env.sh
```

## Running Python Components

With the virtual environment activated, you can now run Python components:

```
python3 plugins/pnt/collector.py
```

## Deactivating the Environment

To exit the virtual environment:

```
deactivate
```

## Windows-Specific Issues

### SecurityError when running the activate scripts function

This happens because of some permission issues on Windows/WSL.

**Temporary Fix** (will have to do everytime):
```
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

**Permanent Fix** (only have to do once):
```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Run either command and then re-run from `python3 -m venv pulse-env` and you will have your environment setup.
