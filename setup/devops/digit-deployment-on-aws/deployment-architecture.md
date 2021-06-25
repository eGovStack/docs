# Deployment Architecture

This section contains architectural details about DIGIT deployment. It discusses the various activities in a sequence of steps to provision required infra and deploy DIGIT.

### Sample Kubernetes Architecture

![](../../../.gitbook/assets/image%20%289%29.png)

### DIGIT Deployment Architecture

![](../../../.gitbook/assets/image%20%2812%29.png)

![](../../../.gitbook/assets/image%20%2810%29.png)

### The CI/CD Flow

* Every code commit is well-reviewed and squash merge to branches through Pull Requests.
* Trigger the CI Pipeline that ensures code quality, vulnerability assessments,  CI tests before building the artefacts.
* Artefact is version controlled based on Semantic versioning based on the nature of the change.
* After successful CI, Jenkins bakes the Docker Images with the versioned artefacts and pushes the baked docker image to Docker Registry.
* Deployment Pipeline pulls the built Image and pushes to the corresponding Env.

### Deployment Scripts

* As all the DIGIT services that are containerized and deployed on Kubernetes, we need to prepare deployment manifests. The same can be found [here](https://github.com/egovernments/Train-InfraOps). 
* DIGIT has built helm charts to using the standard helm approach to ease managing the service-specific configs, customisations, switch/toggle, secrets, etc. 
* Golang base Deployment script that reads the values from the helm charts template and deploys into the cluster.       
* Each env will have one master yaml template that will have the definition of all the services to be deployed, their dependencies like Config, Env, Secrets, DB Credentials, Persistent Volumes, Manifest, Routing Rules, etc.. 



 [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)​](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation](https://egov.org.in/) is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

