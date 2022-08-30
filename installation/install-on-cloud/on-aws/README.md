---
description: Provision infra for DIGIT on AWS using Terraform
---

# On AWS

The [**Amazon Elastic Kubernetes Service (EKS)**](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) is one of the AWS services for deploying, managing, and scaling any distributed and containerized workloads. Here we can provision the EKS cluster on AWS from ground up and using an automated way (infra-as-code) using [**terraform**](https://www.terraform.io/intro/index.html) and then deploy the DIGIT Services config-as-code using [**Helm**](https://helm.sh/docs/).

## Pre-reads

* Know about EKS: [https://www.youtube.com/watch?v=SsUnPWp5ilc](https://www.youtube.com/watch?v=SsUnPWp5ilc)
* Know what is terraform: [https://youtu.be/h970ZBgKINg](https://youtu.be/h970ZBgKINg)

## Installation Steps

{% content-ref url="1.-pre-requisites.md" %}
[1.-pre-requisites.md](1.-pre-requisites.md)
{% endcontent-ref %}

{% content-ref url="2.-understanding-eks.md" %}
[2.-understanding-eks.md](2.-understanding-eks.md)
{% endcontent-ref %}

{% content-ref url="3.-setup-aws-account.md" %}
[3.-setup-aws-account.md](3.-setup-aws-account.md)
{% endcontent-ref %}

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="5.-prepare-deployment-config.md" %}
[5.-prepare-deployment-config.md](5.-prepare-deployment-config.md)
{% endcontent-ref %}

{% content-ref url="6.-deploy-digit.md" %}
[6.-deploy-digit.md](6.-deploy-digit.md)
{% endcontent-ref %}

{% content-ref url="7.-bootstrap-digit.md" %}
[7.-bootstrap-digit.md](7.-bootstrap-digit.md)
{% endcontent-ref %}



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
