## CI-CD MicroService Application

### CI/CD Pipeline for microservices:
* Monorepo advantages:
  * Makes the code management and development easier 
  * Clone and work with only 1 repo
  * Changes can be tracked, tested and released together
  * Shared code and configurations (Dockerfile, Docker-compose...)

* Monorepo disadvantages:
  * Tight coupling of projects
  * Easier to break this criterion and develop more tightly coupled code
  * Big source code, means git interactions becomes slow
  * Additional logic necessary to make sure only service is built and deployed which had changes
  * All projects and teams are affected, if there is some issue

* Polyrepo advantages:
  * Code is completely isolated
  * Clone and work on them separately
  * GitLab have projects to configure connected projects together (Groups)
    * Helps to keep an overview
    * Create shared secrets, CI/CD variables, Runners
  * Own Pipeline for a repo

* Polyrepo disadvantages:
  * Cross-cutting changes is more difficult
  * Changes spreaded across projects must be submitted as separate Merge requests instead of having a single, atomic MR
  * Switching between projects tedious
  * Searching, testing and debugging is more difficult
  * Sharing resources is more difficult

### Deploy Micro Services:
* `.deploy script: docker network create micro_service || true &&`
  * 1st time creates network and after creating next line fails. Use "|| true" not to fail
* `docker network ls` - to check network in terminal CI
  * `4c6d1367fe99   micro_service   bridge    local`
* `docker inspect aa0194f7032d` - network config
* `docker inspect aa0194f7032d | grep Network` - NetworkMode & NetworkSettings of frontend container aa0194f7032d
