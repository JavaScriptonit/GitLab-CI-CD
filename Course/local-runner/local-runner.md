To install GitLab Runner using Homebrew:

1. Install GitLab Runner:\
   **brew install gitlab-runner**
   [link](https://docs.gitlab.com/runner/install/osx.html#homebrew-installation-alternative)


2. Install GitLab Runner as a service and start it.\
   **brew services start gitlab-runner:**\
   `Successfully started 'gitlab-runner' (label: homebrew.mxcl.gitlab-runner)`\
   $ gitlab-runner -version === shows the version of GitLab runner\
   $ brew services info gitlab-runner === to check the status\
   `gitlab-runner (homebrew.mxcl.gitlab-runner)`\
   `Running: ✔`\
   `Loaded: ✔`\
   `Schedulable: ✘`\
   `User: andreyshabunov`\
   `PID: 26826`


3. Connect GitLab installation:\
   $ gitlab-runner register
   1. Enter the GitLab instance URL\
      https://gitlab.com/
   2. Enter the registration token:\
      GR1348941c8-hse4jkvJn1E1y**** - from [settings/ci_cd](https://gitlab.com/JavaScriptonit/mynodeapp-cicd-project/-/settings/ci_cd)
   3. Enter a description for the runner:\
      local-runner
   4. Enter tags for the runner (comma-separated):\
      macos, local
   5. Enter optional maintenance note for the runner:\
      This runner uses shell executor
   6. Enter an executor:\
      shell

   $ gitlab-runner list === get the runner’s details


4. [Unregister the runner](https://techdirectarchive.com/2022/04/25/how-to-unregister-a-gitlab-runner/)


5. [Install and Register Windows Runner](https://techworld-with-nana.teachable.com/courses/1769488/lectures/39895937)


6. Stop GitLab Runner:
* `brew services info gitlab-runner ` - brew services info
* `brew services list` - brew services status check
* `brew services stop gitlab-runner` - Stopping gitlab-runner
* 


