---
description: >-
  Quickstart Installation helps you jump start with the DIGIT basic installation
  steps with the limited functionalities.
---

# Quickstart

## Demo/Evaluation Installations

Quickstart solutions that you give you the ability to try setting up DIGIT Infra quickly. These are not meant for production use as is.

If you want to install DIGIT on Lightweight Kubernetes ([k3d](https://github.com/rancher/k3d) ) for proofs of concept, see the open source project [k3d](https://github.com/rancher/k3d).  You can install DIGIT in a local or cloud VM when you have all the below pre-requisites and hardware requirement.

### Requirements

To use k3d, make sure your instance meets the following requirements:

* **Linux distribution** running in a VM or bare metal
  * Ubuntu 18.04 or Debian 10 (VM or bare metal)
  * 2 vCPUs (recommend 4)
  * 8GiB of RAM (recommend 16)
  * 30GiB of HDD (recommend 40+)
  * NAT or Bridged networking with access to the internet
  * Install `curl`, `wget` `git`, and `tar` (if they're not already installed):
    * `sudo apt-get install curl git wget tar`
  * Install [Docker](https://docs.docker.com/engine/install/ubuntu/)
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) on Linux
  * Open terminal and Install k3d(v4.4.8) on Linux using the below command
    * `wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | TAG=v4.4.8 bash`           &#x20;
*   **OSX**

    * Docker Desktop local Kubernetes cluster enabled
    * At least 6 GiB of memory allocated to Docker Desktop
    * Install [Docker Desktop](https://docs.docker.com/docker-for-mac/install/) and local Kubernetes cluster enabled
    * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/) on Mac
    * Install k3d(v4.4.8) on Mac, on terminal use [Homebrew](https://brew.sh) (Homebrew is available for MacOS) using the below command
      * `brew install k3d` &#x20;

    ****
* **Windows 10 or above**
  * [Docker Desktop for windows](https://docs.docker.com/docker-for-windows/install/#system-requirements-for-wsl-2-backend) need to be installed
  * [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) on Windows
  * [Install Chocolatey](https://chocolatey.org) package manager for windows
  * Install [GitBash](https://git-scm.com/download/win) as an alternative command prompt that allows most of the Linux commands on windows.
  * Now open gitbash and Install k3d(v4.4.8) on Windows using the below command
    * `choco install k3d`

## Quickstart Setup

When the above prerequisites are met, please proceed with the following steps

{% content-ref url="quickstart/1.-infra-local-setup-k3d.md" %}
[1.-infra-local-setup-k3d.md](quickstart/1.-infra-local-setup-k3d.md)
{% endcontent-ref %}

{% content-ref url="quickstart/2.-deployment.md" %}
[2.-deployment.md](quickstart/2.-deployment.md)
{% endcontent-ref %}

