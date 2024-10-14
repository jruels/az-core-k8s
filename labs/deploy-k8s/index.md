# Creating an AKS cluster and exploring the resources

# Part 1: Introduction and Setup for Azure Kubernetes Service (AKS)

## Introduction

### **Overview of the Lab Objectives**
- Set up an Azure Kubernetes Service (AKS) cluster using Azure CLI.

### **Brief on the AKS Architecture**
- **Azure Kubernetes Service (AKS)**: Managed Kubernetes service for deploying, managing, and scaling containerized applications.
- **Azure CLI**: Command-line tool for managing Azure resources.

### **Tools and Technologies Required**
- **Azure CLI**: Command-line tool for managing Azure resources.
- **Azure Subscription**: Required to create and manage Azure resources.

### **Cloud Shell**
Cloud Shell is a built-in terminal with many standard tools like `az`, `helm`, and `kubectl`. We are using it for this lab.
- Open Cloud Shell by clicking the square with a greater than arrow to the right of the "Copilot" button. 
- Clone the class page that includes all the required manifests. 
```bash
git clone https://github.com/jruels/az-core-k8s.git
```

## Create an AKS Cluster
- Replace **myResourceGroup** with your student resource group **<student#>-rg** and **myAKSCluster** with **<student#>AKSCluster**.

```bash
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 2 \
  --enable-addons monitoring \
  --generate-ssh-keys
```
- **Note:** This command can take up to 10 minutes to complete.

### **Authenticate to the AKS Cluster**

```bash
az aks get-credentials --resource-group <myResourceGroup> --name <student#>myAKSCluster
```

- This command configures `kubectl` to use your credentials for the AKS cluster.

### **List System Pods in the AKS Cluster**

```bash
kubectl get pods --namespace kube-system
```

- This command lists the system pods running in the `kube-system` namespace of the AKS cluster.
- The kube-system namespace is used by Kubernetes to manage system-level components, such as networking and cluster services, including the core DNS, the Kubernetes dashboard, and the API server.

### **View the AKS Cluster in the Azure Portal**
- Open the [Azure Portal](https://portal.azure.com/).
- Navigate to "Resource groups" in the left-hand menu.
- Select your resource group.
- Click on the AKS cluster to view its details.


### **Familiarize Yourself with the AKS Cluster**
- Take some time to explore the different resources and settings within the AKS cluster. For instance:
  - **Node Pools**: View the nodes that make up the AKS cluster.
  - **Workloads**: Check the deployed workloads, including deployments, pods, and replica sets.
  - **Services and Ingress**: Review the services and ingress controllers that manage network traffic.
  - **Storage**: Examine the storage options, including persistent volume claims and storage classes.
  - **Monitoring**: Explore the monitoring tools and metrics available for the cluster.
  - **Access Control (IAM)**: Review the role-based access control (RBAC) settings and permissions.

# Part 2: Getting familiar with the cluster

## Commands and Namespaces

## Lab Objectives

This lab has you run several commands to familiarize yourself with `kubectl`.

## Lab Structure - Overview 

1. List Kubernetes Pods and Nodes
2. List Kubernetes Services and Namespaces
3. Look at Kubernetes components 

### List Pods and Nodes

1. Enter the following to list Pods in the `default` namespace

```
kubectl get pods 
```

**NOTE: This will return 'no resources found'**

2. List Pods in all namespaces.

```
kubectl get pods --all-namespaces
```

3. List nodes

```
kubectl get nodes 
```

4. List nodes and additional information (labels, name, IP etc.) 

```
kubectl get nodes -o wide 
```

### List Services and Namespaces

1. List Services in `default` namespace

```
kubectl get services
```

2. List Services in all namespaces.

```
kubectl get services --all-namespaces
```

**PROTIP: substitute `svc` for `services`**

3. List Namespaces

```
kubectl get namespaces
```

4. Create a new Namespace..  Use `kubectl create --help` if you get stuck. 

### Explore Kubernetes

Using `kubectl` interact with the Kubernetes cluster. 

1. Look at documentation

```
kubectl --help
```

2. Retrieve information about Kubernetes resources

```
kubectl get <random resources>
```

3. Look at node details

```
kubectl describe node <node from cluster>
```

4. Look at Pod details 

```
kubectl describe pod -n kube-system coredns
```

5. Check out service details

```
kubectl describe svc kubernetes
```

6. Look at deployment details

```
kubectl describe deployment -n kube-system coredns 
```

Now you should have a better understanding of Kubernetes resources and using the `kubectl` client.
