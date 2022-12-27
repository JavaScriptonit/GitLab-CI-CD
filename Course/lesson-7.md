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

### Clean runner from containers, images and network to have FRESH state with Docker and Docker-compose installed:
* `docker images` - check images
  * `docker rmi 9fc5b1ea74c7 0c6e70abf54f cd4727472014` - remove images
* `docker ps` - check running containers
  * `docker stop 9fc5b1ea74c7 9fc5b1ea74c7 9fc5b1ea74c7` - stop running containers
* `docker ps -a` - check CONTAINERS
  * `docker rm fe6e704938c4 ccd9a5509a62 4734755351ed` - remove containers
* `docker network ls` - check
  * `docker network rm micro_service` - remove

### 2 Templates Types: 
* Pipeline templates
  * e2e CI/CD workflow
  * used by itself with no other .gitlab-ci.yml file
* Job templates
  * provides specific jobs
  * included to CI/CD workflow
* include:
  * `- local` - reference from same repository
  * `- file` - reference from another private project (same GitLab instance)
  * `- remote` - include from a different location (full URL necessary)
  * `- template` - include GitLab's templates

