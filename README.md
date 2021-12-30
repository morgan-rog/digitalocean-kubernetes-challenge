# Digital Ocean Kubernetes Challenge 2021 - Project: Deploy scalable NoSQL Database (MongoDB) Cluster

## About Me
I am a student studying computer science and a cloud automation engineer intern. I am a beginner
and  I wanted to learn more about DigitalOcean and Kubernetes. I took this challenge and had a
lot of fun!

## Installing Prerequisites
Before provisioning a Kubernetes cluster on DigitalOcean I needed to install [doctl](https://docs.digitalocean.com/reference/doctl/how-to/install/) and
[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/). I used the
Windows installation for both.
I also needed to connect **doctl** to my account and the confirmation message is seen below:
![doctl-account-confirmation](/screenshots/doctl-account-confirmation.PNG)
**doctl** was used to connect to the K8s cluster after it was provisioned on Digital Ocean
and **kubectl** was used to interact with the K8s cluster and to apply the MongoDB
configurations.

## Creating a K8s Cluster on DigitalOcean
1. Go to DigitalOcean Dashboard and click 'Kubernetes'
2. I left Kubernetes version to default
3. VPC Network set to default
4. Set 'Node Plan' to 1 GB RAM(2 GB Total)/1vCPU since I used this cluster for the challenge only
![create-k8-cluster-1](/screenshots/create-k8-cluster-1.PNG)
5. Named my cluster 'morganrog-kubernetes-challenge'
![create-k8-cluster-finalize-2](/screenshots/create-k8-cluster-finalize-2.PNG)
6. Click 'Create Cluster'
7. Provisioning the K8s cluster takes a few minutes and then we can connect to it using **doctl**
![create-k8-cluster-provisioning-3](/screenshots/create-k8-cluster-provisioning-3.PNG)
![provisioned-k8-cluster-digitalocean](/screenshots/provisioned-k8-cluster-digitalocean.PNG)

## Connecting to the K8s cluster we provisioned on DigitalOcean
After the K8s cluster has been provisioned we can connect to it using a command that is presented to us on the dashboard:
![connecting-to-cluster](/screenshots/connecting-to-cluster.PNG)

## Deploy MongoDB Cluster
Now we can set up the configuration files for our MongoDB cluster!
* We need to create 4 K8s configuration files:
    * ConfigMap - MongoDB Endpoint
    * Secret - MongoDB User & Password
    * Deployment and Service - MongoDB Application with internal Service

## The files
1. ConfigMap -> mongo-config.yaml
    * this file is our ConfigMap which will be our MongoDB Endpoint 

![mongo-config-yaml](/screenshots/mongo-config-yaml.PNG)

2. Secret -> mongo-secret.yaml
    * this file is where we set up the username and password for the MongoDB

![mongo-secret-yaml](/screenshots/mongo-secret-yaml.PNG)

3. Deployment and Service -> mongo.yaml
    * this file contains the Deployment and Service configurations for the MongoDB
    * We put the Deployment and Service in 1 file because they belong together

![mongo-yaml](/screenshots/mongo-yaml.PNG)

* The 'template' is the configuration for the pod and I used the [official](https://hub.docker.com/_/mongo?tab=description&page=1&name=5.0) mongo
    image from dockerhub with the image name of '5.0'
* The port number needs to be set to '27017'
* The image I used creates both a MongoDB username and password when created so I set
those environment variables to the secrets we created in the mongo-secret.yaml file

![mongotemplate](/screenshots/mongotemplate.PNG)
![mongotemplate-port-and-env-variables](/screenshots/mongotemplate-port-and-env-variables.PNG)



# Deployment and Service in 1 file because they belong together
# kind - "deployment"
# template - configuration for Pod
# Deployment manages Pod
# Label - you can give any K8s component a label
# labels are key value pairs that are attached to K8 resources
# all pods can share the same label
# Selector - selects pods to forward the request to
