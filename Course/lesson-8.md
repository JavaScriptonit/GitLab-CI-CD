## Deploy Microservices to Kubernetes cluster:

### Create a K8s cluster on Google Cloud:
* [Creating a cluster (Google Cloud project)](https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/11628212#overview)
* OR [Creating a cluster (LKE project)](https://techworld-with-nana.teachable.com/courses/1769488/lectures/39916812)
  * download and install [gcloud CLI](https://cloud.google.com/sdk/docs/install-sdk) 
  * `./google-cloud-sdk/install.sh` - install script to add gcloud CLI tools to your PATH
  * `gcloud init` - initialize the gcloud CLI
  * log in using your Google user account
  * 
* [Google Cloud Cluster](https://console.cloud.google.com/kubernetes/clusters/details/me-west1/autopilot-cluster-1/details?project=fluent-oarlock-358313)
  * `gcloud auth list` - List accounts whose credentials are stored on the local system
  * `gcloud config list` - List the properties in your active gcloud CLI configuration
* [Enable the Google Kubernetes Engine API](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#default_cluster_kubectl)
* `gcloud container clusters get-credentials autopilot-cluster-1 --region me-west1 --project fluent-oarlock-358313` - Update the kubectl configuration to use the plugin
* `gke-gcloud-auth-plugin --version` - Check the gke-gcloud-auth-plugin binary version
* `kubectl get namespaces` - Verify the configuration
* `kubectl config view` - To view your environment's kubeconfig
* `kubectl cluster-info` - connect to cluster and get info from it


### Create dedicated user and permissions:
* `kubectl create namespace my-micro-service` - create namespace
  * namespace/my-micro-service created
* `kubectl create serviceaccount cicd-sa --namespace=my-micro-service` - create service account
  * serviceaccount/cicd-sa created
* `vim cicd-role.yaml` - create cicd-role.yaml with role rules
* `kubectl apply -f cicd-role.yaml` - create role
  * role.rbac.authorization.k8s.io/cicd created
* `kubectl create rolebinding cicd-rb --role=cicd-role --serviceaccount=my-micro-service:cicd-sa --namespace=my-micro-service` - bind role with rules
  * rolebinding.rbac.authorization.k8s.io/cicd-rb created

### Create Kubeconfig file:
* [Install kubectl and configure cluster access](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl#default_cluster_kubectl)
* [Install the Google Cloud CLI](https://cloud.google.com/sdk/docs/install-sdk)
* `cp ~/Downloads/kubeconfig.yaml ~/cicd-kubeconfig.yaml` - copy kubeconfig file
* `vim cicd-kubeconfig.yaml` - replace values (admin user) and token
  * `kubectl get serviceaccount -n my-micro-service` - get serviceaccount name and created secret with token
  * `kubectl get serviceaccount cicd-sa -n my-micro-servce -o yaml` - get serviceaccount secret name
  * `kubectl get secret cicd-sa-token-4fkgn -n my-micro-servce -o yaml` - get full secret value with token
  * `echo "cicd-sa-token-4fkgn token value" | base64 -D` - decode command
* `export KUBECONFIG=cicd-kubeconfig.yaml` - to get new permissions
  * `kubectl get namespace` - to test new permissions (should be forbidden)
  * `kubectl get service -n my-micro-service` - to test new permissions (should be not forbidden)
* ADD variable to a group of projects [mymicroservice-cicd](https://gitlab.com/groups/mymicroservice-cicd33/-/settings/ci_cd)
#### [Manually create an API token for a ServiceAccount:](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)
* `kubectl create token build-robot` - The output from that command is a token that you can use to authenticate as that ServiceAccount



### Resources:

[Configure ServiceAccount](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account)\
[Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)\
[Namespaces explained by Nana](https://youtu.be/K3jNo4z5Jx8)\
[Role for giving permissions](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)