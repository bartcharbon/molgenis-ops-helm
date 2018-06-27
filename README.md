# MOLGENIS Helm templates

These are the Helm templates that we will use for MOLGENIS operations. Basic concepts in respect to docker you need to know.

**Deployments**

Are a set of pods that will be deployed according to configuration that is usually managed bij Helm. These pods interact with eachother by being in the same namespace created by kubernetes according to the deployment configuration. 

**Pods**

A pod is wrapper around a container. It will recreate the container when it is shutdown for some reason and interact with other pods when needed.

**Containers**

A container is a docker-container that is created from a docker image. It could be seen as an VM for example

**Images**

An image is a template for a container some sort of boot script but also contains the os for example. A build dockerfile, if you will.

**Prerequisites**

There are some prerequisites you need.

- docker
- minikube
 
## Kubernetes

When you want to use kubernetes there are some commands you need to know. Also running on a remote cluster will be a must have to control your whole DTAP.

### Useful commands

Commands that can be used to get information from a kubernetes cluster

- ```kubectl get pods```
  
  Gets alls running instances of containers from a certain deployment
- ```kubectl get services```
  
  Gets all services from a deployment
- ```kubectl get pv```
  
  Gets all persistant volumes
- ```kubectl get pvc```
  
  Gets all persistent volume claims
- ```kubectl get deployments```
  
  Gets all deployments (comparable with docker-compose)

## Remote clusters

When you want to see what is running on the clusters at the CIT you have to make a context switch.
You can access the cluster with kubeconfig-files. You can obtain these by downloading them from the 
MOLGENIS kubernetes cluster.

- Go to https://rancher.molgenis.org:7443 and login
- Go to Rancher --> Cluster: *#name#* --> *Kubeconfig File*
- Go to a **Terminal** where ```kubectl``` is available
- Add this configuration to ~/.kube/config (or place a new file besides this one)
  
  *Example*: 
```bash
# When you added the MOLGENIS configuration to the original configuration
kubectl config user-context molgenis

# or when you placed the MOLGENIS configuration besides the original one
kubectl config use-context molgenis --kubeconfig=*full path to molgenis config*
```
- You can now access all facilities of the MOLGENIS cluster like it is running locally
  
  *Example:*
```bash
kubectl get pods --namespace=*#namespace of application#*

```

## Helm

### Useful commands



- ```helm install .```
  
  Do it in the root of the project where the Chart.yaml is located
  It installs a release of a kubernetes stack. You also store this as an artifact in a kubernetes repository
- ```helm list```
  
  Lists all installed releases
- ```helm delete #release#a```
  
  Performs a sort of mvn clean on your workspace. Very handy for zombie persistent volumes or claims.