---
description: >-
  Quickstart Installation helps you jump start with the DIGIT basic installation
  steps with the limited functionalities.
---

# Quickstart

## Demo/Evaluation Installations

DIGIT Quickstart setup give you the ability to try setting up DIGIT Infra on a local machine/VM quickly. These are not meant for production use as is. However this quickstart flow can make you familiar with most of the production grade setup.

Quickstart is recommended for a basic infra types like local machine, setting up on a single VM, etc. Here we would create a Lightweight Kubernetes ([k3d](https://github.com/rancher/k3d) ) cluster which does not really need full fledged cloud setup or multiple VMs. See the open source project [k3d](https://github.com/rancher/k3d) to understand more.  You can install k3d on a local or on a VM when you have all the below pre-requisites and hardware requirement met.

### H/W Prerequisites:

To install k3d, make sure your instance meets the following h/w requirements that has sufficient CPU and Memory for both your default systems and for the DIGIT Setup requirement

* Apart from the regular system usage, DIGIT should have a dedicated CPU/Memory requirement as below.&#x20;
* You must have a admin/[sudoer](https://medium.com/kernel-space/linux-fundamentals-a-to-z-of-a-sudoers-file-a5da99a30e7f) access before you proceed.
* OS: Ubuntu 18.04 or Debian 10 or Windows 10 or Mac OSX&#x20;
* Local machine or VM or bare metal
* 8 vCPUs (recommend 8+)
* 16 GiB of RAM (recommend 20+)
* 30 GiB of HDD (recommend 40+)
* NAT or Bridged networking with access to the internet

**Before proceeding with DIGIT quickstart. Check the machine's remaining CPU/Memory capacity, To check the same you can use the following commands to determine, the commands vary from an OS to OS, so do choose your OS specific Instructions.**&#x20;

<details>

<summary>Windows - On Command Prompt</summary>

`systeminfo |find "Physical Memory"`

</details>

<details>

<summary>Linux - On Terminal</summary>

`free -m`

</details>

<details>

<summary>Mac - On terminal</summary>

**To Check Memory**: `top -l 1 -s 0 | grep PhysMe`

`Sample Output:` PhysMem: 16G used (3855M wired), 273M unused. &#x20;

(Here memory is not sufficient, it should at least be 8GB)



**To Check CPU:** `top -l 2 | grep -E "^CPU"`

`Sample Output:` \
``CPU usage: 8.46% user, 12.86% sys, 78.66% idle \
``CPU usage: 10.94% user, 8.11% sys, 80.93% idle

Here the CPU is sufficient where >30% is left over for the DIGIT setup to be done.

</details>

{% hint style="info" %}
**Note:** The **above** commands output will provide you with the total memory/cpu and unused/free/available memory/cpu details. **Make sure your unused/free/available** **memory should meet the following**

* Memory: 8GB
* CPU: >30%
{% endhint %}

****

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
