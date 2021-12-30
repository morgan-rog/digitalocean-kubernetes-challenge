# Digital Ocean Kubernetes Challenge 2021 - Project: Deploy scalable NoSQL Database (MongoDB) Cluster

## About Me
I am a student studying computer science and a cloud automation engineer intern. I wanted to
learn more about DigitalOcean and Kubernetes so I took this challenge and had a lot of fun!

## Installing Prerequisites
Before provisioning a Kubernetes cluster on DigitalOcean I needed to install [doctl](https://docs.digitalocean.com/reference/doctl/how-to/install/) and
[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/). I used the
Windows installation for both.
I also needed to connect **doctl** to my account and the confirmation message is seen below
![doctl-account-confirmation](/screenshots/doctl-account-confirmation.PNG)
**doctl** was used to connect to the K8s cluster after it was provisioned on Digital Ocean
and **kubectl** was used to interact with the K8s cluster and to apply the MongoDB
configurations.

## Creating a K8s Cluster on DigitalOcean
1. Go to DigitalOcean Dashboard and click 'Kubernetes'
2. Click the 'Create' button
3. 


* Create 4 K8s config files
    * ConfigMap - MongoDB Endpoint
    * Secret - MongoDB User & Pwd
    * Deployment and Service - MongoDB Application with internal Service

# Deployment and Service in 1 file because they belong together
# kind - "deployment"
# template - configuration for Pod
# Deployment manages Pod
# Label - you can give any K8s component a label
# labels are key value pairs that are attached to K8 resources
# all pods can share the same label
# Selector - selects pods to forward the request to
