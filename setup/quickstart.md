---
description: >-
  Quickstart Installation helps you jump start with the DIGIT basic installation
  steps with the limited functionalities.
---

# Quickstart

## Demo/Evaluation Installations

DIGIT Quickstart setup give you the ability to try setting up DIGIT Infra on a local machine/VM quickly. These are not meant for production use as is. However this quickstart flow can make you familiar with most of the production grade setup.

Quickstart is recommended for a basic infra types like local machine, setting up on a single VM, etc. Here we would create a Lightweight Kubernetes ([k3d](https://github.com/rancher/k3d) ) cluster which does not really need full fledged cloud setup or multiple VMs. See the open source project [k3d](https://github.com/rancher/k3d) to understand more.  You can install k3d on a local or on a VM when you have all the below pre-requisites and hardware requirement met.

### H/W Requirements

To install k3d, make sure your instance meets the following h/w requirements, and You must have a admin/[sudoer](https://medium.com/kernel-space/linux-fundamentals-a-to-z-of-a-sudoers-file-a5da99a30e7f) access before you proceed.

* OS: Ubuntu 18.04 or Debian 10 or Windows 10 or Mac OSX&#x20;
* Local machine or VM or bare metal
* 2 vCPUs (recommend 4)
* 8GiB of RAM (recommend 16)
* 30GiB of HDD (recommend 40+)
* NAT or Bridged networking with access to the internet

## Let's start Quickstart Setup

When the above prerequisites are met, please proceed with the following steps

{% content-ref url="quickstart/1.-infra-setup.md" %}
[1.-infra-setup.md](quickstart/1.-infra-setup.md)
{% endcontent-ref %}

{% content-ref url="quickstart/2.-deployment.md" %}
[2.-deployment.md](quickstart/2.-deployment.md)
{% endcontent-ref %}

{% content-ref url="quickstart/faq.md" %}
[faq.md](quickstart/faq.md)
{% endcontent-ref %}
