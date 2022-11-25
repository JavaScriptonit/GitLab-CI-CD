## [Job build_image - error](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/jobs/3358184415)

## [Course video with unresolved error](https://techworld-with-nana.teachable.com/courses/1769488/lectures/39899011)

### Executing "step_script" stage of the job script:

`$ docker build -t registry.gitlab.com/javascriptonit/mynodeapp-cicd-project:1.0 .`

### Logs:

`Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/build?buildargs=%7B%7D&cachefrom=%5B%5D&cgroupparent=&cpuperiod=0&cpuquota=0&cpusetcpus=&cpusetmems=&cpushares=0&dockerfile=Dockerfile&labels=%7B%7D&memory=0&memswap=0&networkmode=default&rm=1&shmsize=0&t=registry.gitlab.com%2Fjavascriptonit%2Fmynodeapp-cicd-project%3A1.0&target=&ulimits=null&version=1": dial unix /var/run/docker.sock: connect: permission denied`

### [docs.gitlab.com/ - Solution:](https://docs.gitlab.com/ee/ci/docker/using_docker_build.html)
Enable Docker commands in your CI/CD jobs:
* Use the shell executor
    * Install GitLab Runner
    * Register a runner. Select the shell executor
    * On the server where GitLab Runner is installed, install Docker Engine. View a list of supported platforms
    * Add the gitlab-runner user to the docker group: `$ sudo usermod -aG docker gitlab-runner`
    * Verify that gitlab-runner has access to Docker: `$ sudo -u gitlab-runner -H docker info`
    * In GitLab, to verify that everything works, add docker info to .gitlab-ci.yml: 
      * `before_script:`
      * `- docker info`
      * `build_image:`
      * `script:`
      * `- docker build -t my-docker-image .`
      * `- docker run my-docker-image /script/to/run/tests`

### [Job succeeded. Logs:](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/jobs/3371676279)

gitlab-runner check: `$ groups gitlab-runner`
* gitlab-runner : gitlab-runner
* gitlab-runner : gitlab-runner docker
