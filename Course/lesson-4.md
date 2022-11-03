## GitLab Architecture

### GitLab Runners for running the jobs:
1. GitLab Server (GitLab Instance/ GitLab Installation) - is the main component of GitLab architecture
2. GitLab Runners execute the jobs
3. Gitlab.com - server to run the jobs with Runners
4. Different executor types :
   1. Shell executor
   2. Docker executor
   3. Virtual machine executor
   4. Kubernetes executor
   5. Docker machine executor
   6. SSH executor
   7. Parallels executor
   8. VirtualBox executor
5. To make multiple executors on the same host or the same server - register multiple runners on the same host\
To have 10 runners on 1 machine with its own executor - [GitLab Executors](https://techworld-with-nana.teachable.com/courses/1769488/lectures/39894185)