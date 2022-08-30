# CI/CD Build Job Pipeline Setup

&#x20;**On this page:**

* [Integrating services to CI/CD](ci-cd-build-job-pipeline-setup.md#integrating-services-to-ci-cd)
* [Continuous Integration (CI)](ci-cd-build-job-pipeline-setup.md#continuous-integration-ci)
* [Continuous Deployment (CD)](ci-cd-build-job-pipeline-setup.md#continuous-deployment-cd)

Since there are many DIGIT services and the development code is part of various git repos, one needs to understand the concept of **cicd-as-service** which is open-sourced. This page guides you through the process of creating a CI/CD pipeline.



{% embed url="https://youtu.be/87RWvE4Jgpw" %}

## Integrating Services To CI/CD



The initial steps for integrating any new service/app to the CI/CD are discussed below.

Once the desired service is ready for integration: decide the service name, type of service, and if DB migration is required or not. While you commit the source code of the service to the git repository, the following file should be added with the relevant details which are mentioned below:

**Build-config.yml** – It is present under the build directory in the repository

```
https://raw.githubusercontent.com/egovernments/DIGIT-OSS/master/build/build-config.yml
```

This file contains the below details used for creating the automated Jenkins pipeline job for the newly created service.

```
config:
 -   name: < Name of the job, foo/bar would create job named bar inside folder foo >
     build:
     - work-dir: < Working directory of the app to be built >
       dockerfile: < Path to the dockerfile, optional, assumes dockerfile in working directory if not provided >
       image-name: < Docker image name should be similar to your helm chart name >
```

While integrating a new service/app, the above content needs to be added to the build-config.yml file of that app repository. For example: to onboard a new service called **egov-test,** the build-config.yml should be added as mentioned below.

```
config:  
- name: builds/DIGIT-OSS/core-services/egov-test     
  build:     
  - work-dir: egov-test      
    dockerfile: build/maven/Dockerfile       
    image-name: egov-test
```

If a job requires multiple images to be created (DB Migration) then it should be added as below,

```
config:   
- name: builds/DIGIT-OSS/core-services/egov-test     
  build:     
  - work-dir: egov-test       
    dockerfile: build/maven/Dockerfile       
    image-name: egov-test     
  - work-dir: egov-test/src/main/resources/db       
    dockerfile: egov-test/src/main/resources/db/Dockerfile       
    image-name: egov-test-db
```

**Note -** **If a new repository is created then the build-config.yml is created under the build folder and the config values are added to it.**

**The git repository URL is then added to the Job Builder parameters**

When the Jenkins Job => job builder is executed, the CI Pipeline gets created automatically based on the above details in build-config.yml. Eg: **egov-test** job is created in the **builds/DIGIT-OSS/core-services** folder in Jenkins since the “build-config is edited under core-services” And it should be the “master” branch. Once the pipeline job is created, it can be executed for any feature branch with build parameters - specifying the branch to be built (master or feature branch).

As a result of the pipeline execution, the respective app/service docker image is built and pushed to the Docker repository.

**On repo provide read-only access to GitHub users (created while ci/cd deployment )**

## **Continuous Integration (CI)** <a href="#continuous-integration-ci" id="continuous-integration-ci"></a>

The Jenkins CI pipeline is configured and managed 'as code'.

* **Job Builder** – Job Builder is a Generic Jenkins job which creates the Jenkins pipeline automatically which is then used to build the application, create the docker image of it and push the image to the Docker repository. The Job Builder job requires the git repository URL as a parameter. It clones the respective git repository and reads the [**build/build-config.yml**](https://github.com/egovernments/DIGIT/blob/master/core-services/build/build-config.yml) file for each git repository and uses it to create the service build job.

Check and ‌add your repo ssh URL in [**ci.yaml**](https://github.com/egovernments/DIGIT-DevOps/blob/release/deploy-as-code/helm/environments/ci-demo.yaml)​[‌](https://github.com/egovernments/eGov-infraOps/blob/master/helm/environments/ci.yaml)‌

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F3b7e0c5ac4c5064192777b45de690069ff11a674.png?alt=media)

If the git repository ssh URL is available, build the Job-Builder Job.

![](<../../.gitbook/assets/image (305).png>)

If the git repository URL is not available, check and add the same team.

## Continuous Deployment (CD) <a href="#continuous-deployment-cd" id="continuous-deployment-cd"></a>

The services are deployed and managed **on a Kubernetes cluster** in cloud platforms like **AWS, Azure, GCP, OpenStack, etc.** Here, we use **helm charts** to manage and generate the **Kubernetes manifest files** and use them for further deployment to the respective **Kubernetes cluster**. Each service is created as charts which have the below-mentioned files.

```
billing-service/   # Directory – name of the service/app
    |
    |-- Chart.yaml  # A YAML file containing information about the chart
    |-- LICENSE     # OPTIONAL: A plain text file containing the license for the chart
    |-- README.md   # OPTIONAL: A human-readable README file
    |-- values.yaml # The default configuration values for this chart
    |-- templates/  # A directory of templates that, when combined with values, will generate valid Kubernetes manifest files.
            |
            | -- deployment.yaml
            | -- service.yaml 
            | -- ingress.yaml 
```

**Note**: Below steps are only for new services introduction and Implementation.

* To deploy a new service, you need to create a new helm chart for it( refer to the above example). The chart should be created under the **charts/helm** directory in the [**DIGIT-DevOps**](https://github.com/egovernments/DIGIT-DevOps/tree/quickstart/deploy-as-code/helm/charts) repository.&#x20;
* If you are going to introduce a new module with the help of multiple services, we suggest you create a new _Directory_ with your module name.

**Eg**.:-

```
charts/helm/<new_module_name>/<new_service_chart_name-1>
                   |-------- /<new_service_chart_name-2>
                   |-------- /<new_service_chart_name-3>
```

* You can refer to the existing helm chart structure [here](https://github.com/egovernments/DIGIT-DevOps/tree/quickstart/deploy-as-code/helm/charts)

This chart can also be modified further based on user requirements.

The deployment of manifests to the Kubernetes cluster is made very simple and easy. There are Jenkins Jobs for each state and are environment-specific. We need to provide the image name or the service name for the respective Jenkins deployment job.

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2Fe39a9063f0ae56f845ba2230786302c0d4e957e6.png?alt=media)

Enter a caption for this image (optional).

![](https://gblobscdn.gitbook.com/assets%2F-MERG\_iQW5oN4ukgXP8K%2Fsync%2F5e19cdbb9eb18d76fdd2b4f28c5aed5c8bf377e2.png?alt=media)

Enter a caption for this image (optional).

‌The deployment Jenkins job internally performs the following operations:

* Reads the image name or the service name given and finds the chart that is specific to it.
* Generates the Kubernetes manifests files from the chart using the helm template engine.
* Execute the deployment manifest with the specified docker image(s) to the Kubernetes cluster.

[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
