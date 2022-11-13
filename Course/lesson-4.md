## GitLab Architecture

### GitLab Runners for running the jobs:
1. GitLab Server (GitLab Instance/ GitLab Installation) - is the main component of GitLab architecture
2. GitLab Runners execute the jobs
3. Gitlab.com - server to run the jobs with Runners
4. **Different executor types :**
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
6. **Execution Flow:**
   1. **GitLab -> Runner -> Executor**
      1. Runner requests new jobs from GitLab instance (GitLab.com)
      2. Runner compiles and sends the job's payload to Executor
      3. Executor clones sources or downloads artifacts from GitLab instance and executes the job
      4. Executor returns jobs output abd status to the Runner
      5. Runner updates job output and status to GitLab instance
7. **Default Shared Runners:**
   1. By default, GitLab uses one of its shared runners to run your CI/CD jobs
   2. These shared runners are maintained by GitLab
   3. Docker Machine Executors are used for them
      1. `Preparing the "docker+machine" executor` - in Job logs: type, name of executor
8. **Scope of Runners:**
   1. Shared Runners - available to all groups and projects in a GitLab instance (managed by GitLab)
   2. Group Runners - available to all projects in a group
   3. Specific Runners - associated with a specific project (self-managed)
9. **Specify a Docker image that the jobs runs in:**
   1. "image: node:17-alpine" with a specific version
10. **Multiple Runners:**
    1. 1 job runs on a specific runner with configured setup for that job (**flexibility**)
    2. Multiple runners with the same configuration for jobs when 1 of that runners fails (**scalability**)