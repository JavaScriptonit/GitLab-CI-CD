## Core concepts of GitLab CI/CD
[Nana Janashia Project "mynodeapp-cicd-project" Fork](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project)\
[GitLab Pipelines](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/pipelines)

### Pipeline is scripted:
1. Whole logic is scripted in YAML format (.gitlab-ci.yml)
   1. This file contains the whole CI/CD pipeline configuration
2. Jobs
   1. The most basic building block of the GitLab CI/CD pipeline
   2. It is a step in that pipeline (define what to do)
   3. You can define arbitrary names for your jobs
   4. Must contain at least the script clause
   5. script specify the commands to execute
3. Pipeline (\GitLabCICD\.gitlab-ci.yml):
   1. run_tests (stage 1)
   2. build_image (stage 2)
   3. push_image (stage 3)
4. Pipeline logic becomes part of application code. 
   1. GitLab auto detects .gitlab-ci.yml and run any logic written there
   2. Is the whole workflow process or the CI/CD process
5. Stages
   1. You can group multiple jobs into stages that run in a defined order
   2. Multiple jobs in the same stage are executed in parallel
   3. Execute jobs in certain order within a stage:
      1. use "needs" in job - to have a dependency 
      2. make a bash script in .sh file with linux commands
         1. chmod +x prepare-tests.sh - change mode to executable
         2. ./prepare-tests.sh - execute file
   4. Separate jobs for different branches:
      1. use "only" / "except" to control when jobs are executed
   5. Configure the whole pipeline behavior:
      1. use "workfkow:rules" - controls whether or not the whole pipeline is created
      2. use GitLab variables = $CI_COMMIT_BRANCH != "main" - to avoid "only: - main"