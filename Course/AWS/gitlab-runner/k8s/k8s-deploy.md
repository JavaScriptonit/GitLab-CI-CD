### Kubernetes deploy with GitLab Runner:
* `ssh -i ~/Downloads/gitlab-runner-key.pem ubuntu@ec2-3-89-23-9.compute-1.amazonaws.com` - in terminal
* `sudo snap install kubectl` - [install-kubectl-linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
* `sudo apt-get update`
* `sudo apt-get install -y ca-certificates curl`
* Download the Google Cloud public signing key:
  * `sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg`
* Add the Kubernetes apt repository:
  * `echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list`
* Update apt package index with the new repository and install kubectl:
  * `sudo apt-get update`
  * `sudo apt-get install -y kubectl`
* `sudo snap install kubectl --classic` - kubectl 1.26.0 from Canonical✓ installed
* `kubectl` - check installation