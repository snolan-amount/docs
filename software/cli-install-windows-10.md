---
sidebar_label: 'Windows 10'
title: 'Astronomer CLI Installation for Windows 10'
id: cli-install-windows-10
description: Install the Windows-based CLI or the Unix-based CLI a Windows Subsystem for Linux (WSL).
---

Welcome to Astronomer!

If you're a Windows User looking to install and use the Astronomer CLI, you have 2 options:

1. Install the Unix-based CLI on Windows Subsystem for Linux (WSL)
2. Install the Windows-based CLI

> **Note:** Either option will require Windows 10 or greater.

## Astronomer CLI on Windows Subsystem for Linux (WSL)

This guide will walk you through the setup and configuration process for using the Astronomer CLI in the Windows Subsystem for Linux (WSL) on Windows 10. Before you start, make sure:
 - You're running the bash terminal
 - You have [WSL enabled](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
 - You're running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11.

**Note:** We use Ubuntu as our Linux flavor of choice, but this guide should work for other distributions as well.

Find the full WSL installation guide here: [Install WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

### Step 1. Install Docker CE for Windows

Follow the [Docker for Windows Install Guide](https://docs.docker.com/docker-for-windows/install/).

Once you finish this installation, open a new WSL session, using the distro shell or Windows Terminal. You can now run `docker run hello-world` through your WSL instance to ensure everything works as expected.

**Last thing**: Whenever you run Docker-compose up, you'll want to make sure you navigate to the `/c/Users/name/dev/myapplication` first, otherwise your volume won't work. In other words, never access `/mnt/c` directly.

### Step 2. CLI Install

Once you've completed the steps above, head over to our [CLI Quickstart Guide](cli-quickstart.md) to finish the installation and start deployment DAGs.

## Astronomer CLI on Windows 10 (PowerShell)

You can install a Windows adapted version of the Astronomer CLI directly by following the instructions below.

### Step 1. Pre-Flight Checklist

Make sure you have the following installed:

- Windows 10
- [Docker](https://docs.docker.com/docker-for-windows/install/)

### Step 2. Enable WSL-2 Based Docker Engine or Hyper-V (legacy)

Make sure that the WSL 2 based engine is enabled in Docker Settings (preferred). If this is not possible, enable Hyper-V (legacy). This is required to run Docker and Linux Containers.

If you have any issues with Docker, check out [Docker's Troubleshooting Guide for Windows](https://docs.docker.com/docker-for-windows/troubleshoot/).

### Step 3. Download the Astronomer CLI

Currently, Astronomer on Windows outside of WSL is only supported by Astronomer CLI versions 0.8 and beyond.

You can download the latest version of the CLI [here](https://github.com/astronomer/astro-cli/releases/).

### Step 4. Extract the contents

After following step 3, you should see a zip file on your machine that contains the following:

- CHANGELOG
- README
- LICENSE
- A file titled `astro.exe`

Grab that `astro.exe` file and move it to a location that won't be deleted.

### Step 5. Add Executable to Path
Add the location of `astro.exe` in your %PATH%. If you don't know how to do this, check out [this helpful guide](https://helpdeskgeek.com/windows-10/add-windows-path-environment-variable/).

### Step 6. Final Command

Now, open your Terminal or PowerShell console and run the following:

```
C:\Windows\system32>astro version
Astronomer CLI Version: 0.8.2
Git Commit: f5cdab8f832da3c6184a7ac167b491e3bac3c022
```

If you get a response like the above, you're all set! Happy Airflow-ing.

## Potential Postgres Error

As a Windows user, you might see the following error when trying to call `astro dev start` on your newly created workspace:

```
Sending build context to Docker daemon  8.192kB
Step 1/1 : FROM quay.io/astronomer/ap-airflow:latest-onbuild
# Executing 5 build triggers
 ---> Using cache
 ---> Using cache
 ---> Using cache
 ---> Using cache
 ---> Using cache
 ---> f28abf18b331
Successfully built f28abf18b331
Successfully tagged hello-astro/airflow:latest
INFO[0000] [0/3] [postgres]: Starting
Pulling postgres (postgres:10.1-alpine)...
panic: runtime error: index out of range
goroutine 52 [running]:
github.com/astronomer/astro-cli/vendor/github.com/Nvveen/Gotty.readTermInfo(0xc4202e0760, 0x1e, 0x0, 0x0, 0x0)
....
```

This is an issue pulling Postgres that should be fixed by running the following:

```
Docker pull postgres:10.1-alpine
```
