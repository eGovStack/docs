# Infra Best Practices

### Best practices for securing your Kubernetes cluster

Kubernetes has changed the way organizations deploy and run their applications, and it has created a significant shift in mindsets. While it has already gained a lot of popularity and more and more organizations are embracing the change, running Kubernetes in production requires care.

Although Kubernetes is open source and does it have its share of vulnerabilities, making the right architectural decision can prevent a disaster from happening.

You need to have a deep level of understanding of how Kubernetes works and how to enforce the best practices so that you can run a secure, highly available, production-ready Kubernetes cluster.

Although Kubernetes is a robust container orchestration platform, the sheer level of complexity with multiple moving parts overwhelms all administrators.

That is the reason why Kubernetes has a large attack surface, and, therefore, hardening of the cluster is an absolute must if you are to run Kubernetes in production.

There are a massive number of configurations in K8s, and while you can configure a few things correctly, the chances are that you might misconfigure a few things.

I will describe a few best practices that you can adopt if you are running Kubernetes in production. Let’s find out.

### Use a Managed Kubernetes Service if Possible

If you are running your Kubernetes cluster in the cloud, consider using a managed Kubernetes cluster such as [Google Kubernetes Engine](https://cloud.google.com/kubernetes-engine) or [Azure Kubernetes Service](https://azure.microsoft.com/en-us/services/kubernetes-service/).

A managed cluster comes with some level of hardening already in place, and, therefore, there are fewer chances to misconfigure things. A managed cluster also makes upgrades easy, and sometimes automatic. It helps you manage your cluster with ease and provides monitoring and alerting out of the box.

### Upgrade Kubernetes Frequently

Since Kubernetes is open source, vulnerabilities appear quickly and security patches are released regularly. You need to ensure that your cluster is up to date with the latest security patches and for that, add an upgrade schedule in your standard operating procedure.

Having a CI/CD pipeline that runs periodically for executing rolling updates for your cluster is a plus. You would not need to check for upgrades manually, and rolling updates would cause minimal disruption and downtime; also, there would be fewer chances to make mistakes.

That would make upgrades less of a pain. If you are using a managed Kubernetes cluster, your cloud provider can cover this aspect for you.

### Patch and Harden Your OS

It goes without saying that you should patch and harden the operating system of your Kubernetes nodes. This would ensure that an attacker would have the least attack surface possible.

You should upgrade your OS regularly and ensure that it is up to date.

### Enforce RBAC

Kubernetes post version 1.6 has role-based access control \(RBAC\) enabled by default. Ensure that your cluster has this enabled.

You also need to ensure that legacy attribute-based access control \(ABAC\) is disabled. Enforcing RBAC gives you several advantages as you can now control who can access your cluster and ensure that the right people have the right set of permissions.

RBAC does not end with securing access to the cluster by Kubectl clients but also by pods running within the cluster, nodes, proxies, scheduler, and volume plugins.

Only provide the required access to service accounts and ensure that the API server authenticates and authorizes them every time they make a request.

### Use TLS

Running your API server on plain HTTP in production is a terrible idea. It opens your cluster to a man in the middle attack and would open up multiple security holes.

Always use transport layer security \(TLS\) to ensure that communication between Kubectl clients and the API server is secure and encrypted.

Be aware of any non-TLS ports you expose for managing your cluster. Also ensure that internal clients such as pods running within the cluster, nodes, proxies, scheduler, and volume plugins use TLS to interact with the API server.

### Segregate Resources in Namespaces

While it might be tempting to create all resources within your default namespace, it would give you tons of advantages if you use namespaces. Not only will it be able to segregate your resources in logical groups but it will also enable you to define security boundaries to resources in namespaces.

Namespaces logically behave as a separate cluster within Kubernetes. You might want to create namespaces based on teams, or based on the type of resources, projects, or customers depending on your use case.

After that, you can do clever stuff like defining resource quotas, limit ranges, user permissions, and RBAC on the namespace layer.

Avoid binding ClusterRoles to users and service accounts, instead provide them namespace roles so that users have access only to their namespace and do not unintentionally misconfigure someone else’s resources.

Cluster Role and Namespace Role Bindings

### Control Pod to Pod Traffic

You can use Kubernetes network policies that work as firewalls within your cluster. That would ensure that an attacker who gained access to a pod \(especially the ones exposed externally\) would not be able to access other pods from it.

You can create Ingress and Egress rules to allow traffic from the desired source to the desired target and deny everything else.

Kubernetes Network Policy

### Create Separate User Accounts

By default, when you boot your cluster through [kubeadm](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/), you get access to the `kubernetes-admin` config file which is the superuser for performing all activities within your cluster.

Do not share this file within your team, instead, create a separate user account for every user and only provide the right accesses to them. Bear in mind that Kubernetes does not maintain an internal user directory, and therefore, you need to ensure that you have the right solution in place to create and manage your users.

Once you create the user, you can generate a private key and a certificate signing request for the user, and Kubernetes would sign and generate a CA cert for the user.

You can then securely share the CA certificate with the user. The user can then use the certificate within kubectl to authenticate with the API server securely.

Configuring User Accounts

### Follow the Principle of Least Privilege

You can provide granular access to user and service accounts with RBAC. Let us consider a typical organization where you can have multiple roles, such as:

1. Application developers — These need access only to a namespace and not the entire cluster. Ensure that you provide them with access only to deploy their applications and troubleshoot them only within their namespace. You might want application developers with access to spin only ClusterIP services and might wish to grant permissions only to network administrators to define ingresses for them.
2. Network administrators — You can provide network admins access to networking features such as ingresses, and privileges to spin up external services.
3. Cluster administrators — These are sysadmins whose main job is to administer the entire cluster. These are the only people that should have cluster-admin access and only the amount that is necessary for them to do their roles.

The above is not etched in stone, and you can have a different organization policy and different roles, but the only thing to keep in mind here is that you need to enforce the principle of least privilege.

That means that individuals and teams should have only the right amount of access they need to perform their job, nothing less and nothing more.

### Frequently Rotate Infrastructure Credentials

It does not stop with just issuing separate user accounts and using TLS to authenticate with the API server. It is an absolute must that you frequently rotate and issue credentials to your users.

Set up an automated system that periodically revokes the old TLS certificates and issues new ones to your user. That helps as you don’t want attackers to get hold of a TLS cert or a token and then make use of it indefinitely.

A bootstrap token, for example, needs to be revoked as soon as you finish with your activity. You can also make use of a credential management system such as [HashiCorp Vault](https://www.vaultproject.io/) which can issue you with credentials when you need them and revoke them when you finish with your work.

### Use a Partitioned Approach to Secure Secrets

Imagine a scenario where an externally exposed web application is compromised, and someone has gained access to the pod. In that scenario, they would be able to access the secrets \(such as private keys\) and target the entire system.

The way to protect from this kind of attack is to have a sidecar container that stores the private key and responds to signing requests from the main container.

In case someone gets access to your login microservice, they would not be able to gain access to your private key, and therefore, it would not be a straightforward attack, giving you valuable time to protect yourself.

Partitioned Approach

### Limit Resource Usage

The last thing you would want as a cluster-admin is a situation where a poorly written microservice code that has a memory leak can take over a cluster node causing the Kubernetes cluster to crash. That is an extremely important and generally ignored area.

You can add a resource limit and requests on the pod level as a developer or the namespace as an administrator. You can use resource quotas to limit the amount of CPU, memory, or persistent disk a namespace can allocate.

It can also allow you to limit the number of pods, volumes, or services you can spin within a namespace. You can also make use of limit ranges that provide you with a minimum and maximum size of resources every unit of the cluster within the namespace can request.

That will limit users from seeking an unusually large amount of resources such as memory and CPU.

Specifying a default resource limit and request on a namespace level is generally a good idea as developers aren’t perfect. If they forget to specify a limit, then the default limit and requests would protect you from resource overrun.

### Protect Your ETCD Cluster Like a Treasure Vault

The ETCD datastore is the primary source of data for your Kubernetes cluster. That is where all cluster information and the expected configuration is stored.

If someone gains access to your ETCD database, all security measures will go down the drain. They will have full control of your cluster, and they can do what they want by modifying state in your ETCD datastore.

You should always ensure that only the API server can communicate with the ETCD datastore and only through TLS using a secure mutual auth. You can put your ETCD nodes behind a firewall and block all traffic except the ones originating from the API server.

Do not use the master ETCD for any other purpose but for managing your Kubernetes cluster and do not provide any other component access to the ETCD cluster.

Enable encryption of your secret data at rest. That is extremely important so that if someone gets access to your ETCD cluster, they should not be able to view your secrets by just doing a hex dump of your secrets.

### Control Container Privileges

Containers run on nodes and therefore have some level of access to the host file system, however, the best way to reduce the attack surface is to architect your application in such a way that containers do not need to run as root.

Use pod security policies to restrict the pod to access HostPath volumes as that might result in getting access to the host filesystem. Administrators can use a restrictive pod policy so that anyone who gained access to one pod should not be able to access another pod from there.

### Enable Auditing

Audit loggers are now a beta feature in Kubernetes, and I recommend you make use of it. That would help you troubleshoot and investigate what happened in case of an attack.

As a cluster-admin dealing with a security incident, the last thing you would want is that you are unaware of what exactly happened with your cluster and who has done what.

### Conclusion

Remember that the above are just some general best practices and they are not exhaustive. You are free to adjust and make changes based on your use case and ways of working for your team.



 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

