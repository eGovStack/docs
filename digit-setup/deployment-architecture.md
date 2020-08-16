# Deployment Architecture

## Sample Kubernetes Architecture <a id="sample-kubernetes-architecture"></a>

![](https://gblobscdn.gitbook.com/assets%2F-MEQnEQWBZ6Gjip-3pEg%2F-MEagGEBPbhHrfqtuFj8%2F-MEagWEZq89YehJEm_L1%2Fimage.png?alt=media&token=1520af7d-ecb3-481e-9a77-cfe55d28a9cf)

## DIGIT Deployment Architecture <a id="digit-deployment-architecture"></a>

![](https://gblobscdn.gitbook.com/assets%2F-MEQnEQWBZ6Gjip-3pEg%2F-MEeU0YmDS8cWvAHuuWl%2F-MEfwEme5wSwYXoYR1g1%2Fimage.png?alt=media&token=84eec9a6-c81d-4f66-9aa7-1608d7a2c7dc)

![](https://gblobscdn.gitbook.com/assets%2F-MEQnEQWBZ6Gjip-3pEg%2F-MEg1Vrvn-87AM-Y1xEu%2F-MEg7qYKqBZx3v1ySda6%2Fimage.png?alt=media&token=5660b790-329c-4a4a-a782-19019c33e381)

## The CI/CD Flow <a id="the-ci-cd-flow"></a>

* Every codecommit is well reviewed and squash merge to branches through Pull Requests.
* Trigger the CI Pipeline that ensures code quality, vulnerability assessments, CI tests before building the artefacts.
* Artefact are version controlled based on Semantic versioning based on the nature of the change.
* After successful CI, Jenkins bakes the Docker Images with the versioned artefacts and pushes the baked docker image to Docker Registry.
* Deployment Pipeline pulls the built Image and pushes to the corresponding Env.

## Deployment Scripts: <a id="deployment-scripts"></a>

* As all the DIGIT services that are containerized and deployed on kubernetes, we need to prepare deployment manifests. The same can be found [here](https://github.com/egovernments/Train-InfraOps).
* DIGIT has built helm charts to using the standard helm approach to ease managing the service specific configs, customisations, switch/toggle, secrets, etc.
* Golang base Deployment script that reads the values from the helm charts template and deploys into the cluster.
* Each env will have one master yaml template that will have the definition of all the services to be deployed, their dependencies like Config, Env, Secrets, DB Credentials, Persistent Volumes, Manifest, Routing Rules, etc..

