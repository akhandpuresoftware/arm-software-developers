---
processors : ["Neoverse-N1"]
software : ["linux"]
title: "Deploy WordPress example"
type: docs
weight: 3
hide_summary: true
description: >
    Learn how to deploy WordPress example.
---

## Prerequisites

* [An EKS cluster](/content/en/cloud/eks/cluster_deployment.md)

## WordPress Deployment Files
We use three yaml files to deploy WordPress: kustomization.yaml, mysql-deployment.yaml, and wordpress-deployment.yaml.

Lets start with `kustomization.yaml`
```console
secretGenerator:
- name: mysql-pass
  literals:
  - password=YourPasswordHere
resources:
  - mysql-deployment.yaml
  - wordpress-deployment.yaml
```
This file allows us to set passwords for the MySQL database. The resources section selects which files these kustomizations apply to. Information on working with kustomizations is in the [Kubernetes documentation](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/).

The next file is `mysql-deployment.yaml`.
```console

```
This file will deploy a pod with a MySQL container. There are three objects defined. The first object is a Service object. This will create a service called wordpress-mysql. This service will be assigned to be the front end to the MySQL pod through the use of a selector. Therefore, whenever a pod within the cluster wants to communicate with the MySQL pod, it will communicate using the wordpress-mysql service name.

The next object defined (line 16) is a Persistent Volume Claim (PVC). This object is used to mount storage inside the MySQL pod. A key point to understand is that the PVC object is not what creates the storage. It is a declaration of a type of storage that we want available to the cluster. As shown above, we are declaring that we need 20GiB of storage.

The last object created (line 30) is a Deployment. Inside the deployment spec (line 35), we have some selector labels (lines 36-39). Notice that these labels match the labels in the Service object (lines 10-12). This match is what assigns the wordpress-mysql service to the MySQL pod. Within the deployment spec, there is also a pod spec (line 47), where we configure the MySQL container we want deployed in the pod.

The last file is `wordpress-deployment.yaml` which is shown below.
```console

```

Similar to the MySQL yaml, this file creates three objects. First, there is a Service object (line 2) that is named wordpress (line 4). This service exposes port 80 (line 9) and has its type set to LoadBalancer.

The second object is a PVC (line 17). This is similar to what was explained for the MySQL yaml.

The last object is a Deployment (line 31). In the pod spec (line 48), we set the MySQL user and password to match the MySQL non-root user and password in the MySQL yaml file. This password is how WordPress has permission to read/write to the MySQL database pod.

## WordPress Deployment
Navigate to the directory that contains kustomization.yaml, mysql-deployment.yaml, and wordpress-deployment.yaml. Enter the following command to apply above configuration.
```console
kubectl apply -k ./
```

It takes some time for everything to become ready. Let us first check on the volume claims by running the following command.
```console
kubectl get pvc
```

Eventually the volume claims will be bounded to the cluster and appear similar to the image below.

........................................

Next, we can check on the WordPress and MySQL pods by running the following command.
```console
kubectl get pods
```

It may take a little while for the pods to be created and get into the running state. Eventually the pods should look like the image below.

.................................................

Now that the pods are running, we can verify that the persistent volumes have been attached by running the following command.
```console
kubectl get volumeattachments
```
We should see the entry for ATTACHED to be set to true as shown below. This setting means the storage is mounted inside the pods at the mount point declared in the pod specs.

............................................

Verify that the Service is running by running the following command:
```console
kubectl get services wordpress
```
