## Core concepts of GitLab CI/CD

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
   1. run_tests
   2. build_image
   3. push_image