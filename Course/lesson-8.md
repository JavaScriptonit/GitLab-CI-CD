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


### Cluster configuration:
* `kubectl create namespace my-micro-service` - create namespace
  * namespace/my-micro-service created
* `kubectl create serviceaccount cicd-sa --namespace=my-micro-service` - create service account
  * serviceaccount/cicd-sa created
* `vim cicd-role.yaml` - create cicd-role.yaml with role rules
* `kubectl apply -f cicd-role.yaml` - create role
  * role.rbac.authorization.k8s.io/cicd created
* `kubectl create rolebinding cicd-rb --role=cicd-role --serviceaccount=my-micro-service:cicd-sa --namespace=my-micro-service` - bind role with rules
  * rolebinding.rbac.authorization.k8s.io/cicd-rb created
* 