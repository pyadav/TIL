## Kubernetes Local Cluster Setup
For deploying k8s applications on local machine we need a tool to replace 
a fully flagged kubernetes cluster.
there are many options to choose from

- [kind](https://kubernetes.io/docs/tasks/tools/#kind)
- [minikube](https://kubernetes.io/docs/tasks/tools/#minikube)
- [k3s](https://github.com/k3s-io/k3s)

I am using kind for this purpose.
kind creates and manages local Kubernetes clusters using Docker container 'nodes'
 
### Installation
```bash
# Using MacOS so I will be using brew
brew install kind

# Check version of kind 
kind version


# Creating a Cluster will use a default `kindest/node`
# also use the --name flag to assign a diffrent context name`
kind create cluster
kind get clusters
kubectl cluster-info --context <CONTEXT_NAME>

# To specify another image during cluster creation
kind create cluster --image=<IMAGE>

# Deleting a Cluster
kind delete cluster

# Loading an Image Into Your Cluster
# Docker images can be loaded into cluster nodes with
kind load docker-image <IMAGE>

# workflow
docker build -t <IMAGE_NAME>:<TAG_NAME> <DIR>
kind load docker-image <IMAGE_NAME>:<TAG_NAME>
kubectl apply -f <MANIFEST_FILE_IMAGE_TAG>


# Configuring kind Cluster
kind create cluster --config kind-config.yaml
```
