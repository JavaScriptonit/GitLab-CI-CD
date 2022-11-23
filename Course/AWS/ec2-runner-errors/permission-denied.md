## [Job build_image - error](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/jobs/3358184415)

### Executing "step_script" stage of the job script:

`$ docker build -t registry.gitlab.com/javascriptonit/mynodeapp-cicd-project:1.0 .`

### Logs:

`Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/build?buildargs=%7B%7D&cachefrom=%5B%5D&cgroupparent=&cpuperiod=0&cpuquota=0&cpusetcpus=&cpusetmems=&cpushares=0&dockerfile=Dockerfile&labels=%7B%7D&memory=0&memswap=0&networkmode=default&rm=1&shmsize=0&t=registry.gitlab.com%2Fjavascriptonit%2Fmynodeapp-cicd-project%3A1.0&target=&ulimits=null&version=1": dial unix /var/run/docker.sock: connect: permission denied`

### Solution:

`test`
