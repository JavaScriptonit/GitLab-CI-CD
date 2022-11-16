pre steps:
`$ ssh -i ~/Downloads/gitlab-runner-key.pem ubuntu@ec2-44-203-114-204.compute-1.amazonaws.com`

### After local connection to AWS EC2 instance:
* `$ apt-get update` - to update the package before installing the tools
* [Installing GitLab Runner on Linux](https://docs.gitlab.com/runner/install/linux-repository.html)
* `$ curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash`
* `$ sudo apt-get install gitlab-runner` - Install the latest version of GitLab Runner
* `$ sudo gitlab-runner -version`
* `$ sudo gitlab-runner -status`
* `$ sudo gitlab-runner register`
    * url - https://gitlab.com/
    * token - GR1348941c8-hse4jkvJn1E1y****
    * desc - ec2-runner
    * tags - ec2, aws, remote
    * note - The runner is using shell executor
    * executor - shell
* `$ sudo gitlab-runner -start` - restart runner
* `$ sudo apt install nodejs` - after adding tags to any job in .gitlab-ci.yml
* `$ sudo apt install npm` - after adding tags to any job in .gitlab-ci.yml

pre steps:
`$ ssh -i ~/Downloads/gitlab-runner-key.pem ubuntu@ec2-44-204-20-127.compute-1.amazonaws.com` - open CI in terminal

### Register new Runner:
* `$ sudo apt install docker.io` - install Docker on EC2
* `$ sudo docker ps` - use "sudo" to run Docker commands after install Docker
* `$ sudo usermod -aG docker $USER` - [Add your user to the docker group](https://docs.docker.com/engine/install/linux-postinstall/)
* `$ exit` - necessary to restart the virtual machine for changes to take effect
* 