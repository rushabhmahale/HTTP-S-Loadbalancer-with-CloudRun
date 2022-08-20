# HTTP-S-Loadbalancer-with-CloudRun

## Also you can refer [Fargate-ECS-Loadbalancer](https://github.com/rushabhmahale/Fargate-ECS-Loadbalancer.git)

## Why loadbalacer is necessary
Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.

Reffer this doc:- https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/


## What is Cloud Run
Cloud Run is a managed compute platform that lets you run containers directly on top of Google's scalable infrastructure.
You can deploy code written in any programming language on Cloud Run if you can build a container image from it. In fact, building container images is optional. If you're using Go, Node.js, Python, Java, .NET Core, or Ruby, you can use the source-based deployment option that builds the container for you, using the best practices for the language you're using.

Reffer this doc:- https://cloud.google.com/run/docs/overview/what-is-cloud-run

## What is GCR 
A service for storing and managing artifacts in private repositories, including container images, Helm charts, and language packages.

Reffer this doc:- https://cloud.google.com/container-registry/docs/overview

## What is Docker 
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

Reffer this doc:- https://docs.docker.com/get-started/overview/

## What is Containers
Containers are packages of software that contain all of the necessary elements to run in any environment. In this way, containers virtualize the operating system and run anywhere, from a private data center to the public cloud or even on a developer’s personal laptop. From Gmail to YouTube to Search, everything at Google runs in containers. 

Reffer this doc:- https://cloud.google.com/learn/what-are-containers


# Steps to be followed 
## Step 1 create a Doker image
- Go to GCP console open google cloud cli 
![image](https://user-images.githubusercontent.com/63963025/185559986-756aac3c-a682-4d61-9940-3116888b4697.png)

- Create a directory add a html contain inside that directory 
![image](https://user-images.githubusercontent.com/63963025/185728720-b7b36916-ad3e-48ed-8c1d-32a44017e73a.png)
![image](https://user-images.githubusercontent.com/63963025/185728758-e245a242-1499-4c4d-ae52-12eac12c483f.png)


- [index.html](*)

- [Dockerfile](*)
- Format for building docker image 

```
sudo docker build -t <imagename>:<version tag> .
```
- example  
```
sudo docker build -t rushabh-cloudrun-1:v1 .
```
- ![image](https://user-images.githubusercontent.com/63963025/185729865-8c87ac45-8d00-4e02-9c63-a2c1222f4ae9.png)

- lets check image is been build 
```
sudo docker images 
```
- ![image](https://user-images.githubusercontent.com/63963025/185729932-a0e17feb-0b63-4e5f-bd5d-234c621ff022.png)

## Step 2 Create 2 image with another content 
- Go to website folder inside remove index.html append new file cloudrun.html
```
<body bgcolor = '#ADD8E6'>

        <h1>Hello this is Rushabh from Cloud run 2</h1>

</body>
```

- ![image](https://user-images.githubusercontent.com/63963025/185730683-39d6ca58-f10d-47ea-bbda-280a67470f29.png)

- Format for building docker image 

```
sudo docker build -t <imagename>:<version tag> .
```
- example  
```
sudo docker build -t rushabh-cloudrun-2:v2 .
```

- ![image](https://user-images.githubusercontent.com/63963025/185730742-49ad6973-9aae-4c4c-9ae4-3a6e26fa65e9.png)

- ![image](https://user-images.githubusercontent.com/63963025/185730837-95ce7f59-3006-48fb-8be6-f12fb36c5708.png)

## Step 3 Push Docker image to GCR (Google Container Registry)

- This command will login to GCR 
```
gcloud auth configure-docker
```
- ![image](https://user-images.githubusercontent.com/63963025/185730973-911f3a5f-94f0-4ddf-ae70-ac1835a944a7.png)

- Now tag image to push in GCR the Format will be 
```
sudo docker tag <imagename>:<version tag> gcr.io/<project_id>/<image that you want name here>:<version tag>
```
- example
```
sudo docker tag rushabh-cloudrun-1:v1 gcr.io/gcp-xxx-xxxx/rushabh-cloudrun-1:v1
```
- ![image](https://user-images.githubusercontent.com/63963025/185731147-5ef66878-7712-4cc3-aa57-843eeefd926f.png)





