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
![image](https://user-images.githubusercontent.com/63963025/185562954-0876082f-39c3-4aa5-9a02-4bdbbaa66c9b.png)

- [index.html](*)

- [Dockerfile](*)

- ![image](https://user-images.githubusercontent.com/63963025/185563492-cbec3855-c697-4f71-9ea7-86a562d16578.png)

