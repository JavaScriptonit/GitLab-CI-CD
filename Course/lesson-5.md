## Build a real life CI/CD Pipeline for a Node.js application

### Final Pipeline for Node.js Git Project:
* Run Unit Tests
* Run SAST
* Build Docker Image
* Push to Docker Registry
* Deploy to DEV
* Promote to STAGING
* Promote to PROD

### Show reports in GitLab UI (.gitlab-ci.yml):
* use `artifacts:reports:` - to add reports to the Job
* use `junit: app/junit.xml` - to use xml created by jest library
* use `paths: - app/junit.xml` - additional artifact of reports to **DOWNLOAD**

### Packages & Registries:
* Package Registry
  * Use GitLab as a private or public registry for variety of supported package managers
* [Container Registry](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/container_registry)
  * Registry to store Docker images
  * Has all microservices on the project
  * Has all tags for each microservice
    * [Example - microservice/shopping-cart](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/container_registry/3663922)
* Infrastructure Registry 
  * Private registry for laC packages

### Deploy with Docker-compose:
* Useful when run multiple containers
* Everything is defined in one YAML [file](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/blob/main/docker-compose.yaml)
* Spin UP all containers and tear DOWN in 1 single [command](https://github.com/JavaScriptonit/GitLab-CI-CD/blob/main/Course/AWS/ec2-dev-server.md)
