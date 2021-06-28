---
description: >-
  DIGIT is a distributed system, made of many microservices, each intended to be
  scaled, restarted, and configured independently.
---

# Productionize DIGIT

DIGIT provides a great degree of flexibility, and allows to handle massive scale \(transactions/day, managed machines\). However, there is no one-size-fits-all approach for configuring DIGIT; your transactions and usage patterns will need to inform how to prepare your DIGIT deployment to be used in production.

These pages are intended to provide both an intuition for how DIGIT works, as well as concrete tips and advice to make DIGIT more reliable at scale.

## Getting started <a id="getting-started"></a>

Before we can confidently productionize an installation of DIGIT, we need insight into what’s going on. This insight is provided by DIGIT's logs and metrics.

* **Logs**

  In the **Distributed** deployments to Kubernetes, logs are forwarded to whatever [logging solution](https://kubernetes.io/docs/concepts/cluster-administration/logging/) you have configured.

  In the **LocalDebian** deployments, logs are written to `/var/log/containers`.

* **Metrics**

  Follow the to export DIGIT's metrics into a metric store of your choice.



