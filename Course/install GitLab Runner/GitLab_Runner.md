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

3. 

