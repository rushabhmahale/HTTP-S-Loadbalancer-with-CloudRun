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

- Now push image to Google Container Registry 
- Format to push docker image to GCR 
```
docker push gcr.io/<project_id>/<image_name>:<version_tag>
```
- Example
```
 docker push gcr.io/gcp-xxx-xxx/rushabh-cloudrun-1:v1 
```

- ![image](https://user-images.githubusercontent.com/63963025/185779756-838067e0-4635-46f9-84d5-9d467ca64f19.png)

- Push another version image <b> rushabh-cloudrun-2:v2 </b>

```
docker push gcr.io/<project_id>/<image_name>:<version_tag>
```
- Example
```
 docker push gcr.io/gcp-xxx-xxx/rushabh-cloudrun-2:v2
```

- ![image](https://user-images.githubusercontent.com/63963025/185779820-a1b5d9d4-3a6f-4d95-8fb1-f99826927bc1.png)
- Image pushed sucessfully 

- ![image](https://user-images.githubusercontent.com/63963025/185779839-f76a0551-1437-47d0-b03d-b973361bffa6.png)

- Version 1
- ![image](https://user-images.githubusercontent.com/63963025/185779856-174a0206-d3c8-4852-b8ab-1ca2ef95a3bb.png)

- Version 2

- ![image](https://user-images.githubusercontent.com/63963025/185779868-205ea9c7-59e7-4c2a-9c1e-e4fd5b295e78.png)

## Step 4 Create Cloud Run Service

- Search for Cloud run service 
- ![image](https://user-images.githubusercontent.com/63963025/185779968-0aac97c6-c6f6-44b2-bb69-da3baa0eea31.png)

- Create Service 
- ![image](https://user-images.githubusercontent.com/63963025/185780043-67a81ecd-3e72-4a7b-9122-d0735faebd8d.png)

- Now go to GCR (Google Container Registry) >> rushabh-cloudrun-1 >>image Show pull command 

- ![image](https://user-images.githubusercontent.com/63963025/185780249-9f19038b-6e61-4dc9-9241-6bf0648896a4.png)

- Now Copy the container image url
- ![image](https://user-images.githubusercontent.com/63963025/185780304-05d3955b-9509-4dca-bdd7-e527b042334c.png)


-  Remove Docker pull command 
- ![image](https://user-images.githubusercontent.com/63963025/185780376-4160ef26-bb7a-4282-8171-d931799e2544.png)

-  Allow unauthenticated invocations and you can custom your port number given in Dockerfile in my case my port number is 80  
- ![image](https://user-images.githubusercontent.com/63963025/185780815-6eac76ad-53fc-4d63-8227-860747a367bb.png)

-  Cloud run application deployed at port number 80. Now lets check iour webapp is running or not 

- ![image](https://user-images.githubusercontent.com/63963025/185780903-1deb9ef5-0b68-453a-8f46-dd0509eae056.png)

- You can see our application is up and running this for version1 

- ![image](https://user-images.githubusercontent.com/63963025/185780954-e28fa9fe-ad78-45b5-abab-a91c17c321f3.png)

- Cloud run also apply google encryption security to your webpage with SSL certificate

- ![image](https://user-images.githubusercontent.com/63963025/185781116-b649a875-1eb0-4a7e-81b1-2bb3ad366b0d.png)

## What is Google encryption ?
The volume of encrypted web traffic to Google varies by country/region. This chart shows the encryption rate of the top 10 countries/regions for web traffic that Google receives. The variation between countries/regions is due to a number of factors, including the types of devices used in that country/region, as well as the availability of software that can support modern encryption technologies like TLS.

Reffer this link:- https://transparencyreport.google.com/https/overview?hl=en

- Create another revision for Cloud run deploy version 2 application 

- Copy GCR image version tag 2 link 
![image](https://user-images.githubusercontent.com/63963025/185781186-335a2148-2675-4103-b4df-cbefa5deb9a2.png)

- All same default  
- ![image](https://user-images.githubusercontent.com/63963025/185781210-43a580d6-52f4-4e56-83ae-ae20be99d4fb.png)

- ![image](https://user-images.githubusercontent.com/63963025/185781249-dac72332-e7d9-45e6-b72e-53e07018de2f.png)

- Here we go deploying 2nd webapp path <b>/cloudrun</b>
![image](https://user-images.githubusercontent.com/63963025/185781297-bef8d64a-154b-445d-9619-aa89c43ca586.png)


- Now lets Create a Loadbalancer. In the Google Cloud console, go to the Load balancing page. Select HTTP(S) Loadbalancer

![image](https://user-images.githubusercontent.com/63963025/185781871-0e5625bb-49f5-4c63-b60e-bc0644ea0ef8.png)



