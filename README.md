# amazonEKS

![0](https://user-images.githubusercontent.com/45136716/87223844-efe0f280-c39d-11ea-82a7-66005aaa8e1b.jpg)

## What is EKS?

Amazon Elastic Kubernetes Service (Amazon EKS) is a managed service that makes it easy for you to run Kubernetes on AWS without needing to stand up or maintain your own Kubernetes control plane. Kubernetes is an open-source system for automating the deployment, scaling, and management of containerized applications.

EKS is one of the powerful and popular service provided by AWS. Most of the big companies use AWS for setting up their Kubernetes Cluster.

## Let me first share the overview of topics being discussed in these two days of online training....

- Setup an AWS EKS cluster with eksctl
- AWS EKS operations using eksctl
- Helm Package Manager on EKS
- Deploy the Kubernetes Dashboard
- Deploy a stateless sample app
- Deploy a stateful app - using Amazon EBS
- Deploy a stateful app - using Amazon EFS
- Fargate on EKS

![1](https://user-images.githubusercontent.com/45136716/87223850-f5d6d380-c39d-11ea-92f8-d9c96cce9dd0.png)

## Amazon Web Services or aws

AWS is a subsidiary of amazon that provides cloud computing as services, or in other words Infrastructure as a Service (also called IAAS). AWS provides all the computing power(including cpu, ram, gpu) , storage solutions(like ssd), and networking (includes routers, switches, firewall etc) as a services. It is one of the top cloud infrastructure.

## Kubernetes

Kubernetes is a open-source platform for container-orchestration system that is used for automating the process of deploying, scaling, and managing computer applications.

## EKS or Elastic Kubernetes Service

In layman terms we can say that eks is the combination of aws and kubernetes. launching kubernetes on top of aws makes it a powerful tool for automation. EKS is a fully managed service provided by aws for container -orchesration. It uses the computing power of aws to launch computer applications. Many top companies like Intel, HSBC, Snap, GoDaddy and AutoDesk relies on eks to launch their sensitive and critical applications because of its reliability, security, and scalability.

## OwnCloud

OwnCloud is a free and open-source file hosting software for storing, accessing and sharing files, calendars, contacts and emails on the cloud. Since its development in 2010, ownCloud allows creation of private on-demand cloud that offers similar functionalities like those of Dropbox.
Since, you have understood what is aws, eks and owncloud the without further delay let’s start our deployment.

Firstly, we need to setup AWS Command line to perform several operations. For this we need to download AWS command line tool -- https://aws.amazon.com/cli/

Setup the environment variables for aws command line.

![2](https://user-images.githubusercontent.com/45136716/87223954-cb394a80-c39e-11ea-8efb-7bae8581d7f4.jpg)


![3](https://user-images.githubusercontent.com/45136716/87223955-cd030e00-c39e-11ea-8534-bef6e9af019c.jpg)

Although, we can create cluster using aws command but it doesn't provide many options further. Thus, we will use eksctl for creating cluster.

eksctl is a simple CLI tool for creating clusters on EKS - Amazon's new managed Kubernetes service for EC2. It is written in Go, uses CloudFormation, was created by Weaveworks and it welcomes contributions from the community.

For downloading refer to : https://github.com/weaveworks/eksctl

eksctl uses aws credentials file from path - /.aws/credentials

Thus, we need to setup the login credentials for aws command line.

For creating EKS cluster using eksctl we need to create a script for the same. For creating script we can refer to https://eksctl.io/

I am sharing one of the script example with you:

[cluster.yml](https://github.com/ManthanChoudhury/amazonEKS/files/4906750/cluster.yml)

## RUN :--

![5](https://user-images.githubusercontent.com/45136716/87224110-346d8d80-c3a0-11ea-9a12-363e7ada6c5c.jpg)


This command will create a cluster for your desired use.

![6](https://user-images.githubusercontent.com/45136716/87224115-3899ab00-c3a0-11ea-8c93-425871dd28c3.jpg)


Now we need to setup the config file for our AWS cluster for Kubectl....

![7](https://user-images.githubusercontent.com/45136716/87224117-3afc0500-c3a0-11ea-879e-fbfab3497b6f.jpg)


Our cluster is being created. Now, we can use it as per our requirements. Although we can directly use it for deployments but it is better way to setup a separate namespace for our project.

![8](https://user-images.githubusercontent.com/45136716/87224120-44856d00-c3a0-11ea-903d-7c8f3e9c1756.jpg)

![9](https://user-images.githubusercontent.com/45136716/87224123-46e7c700-c3a0-11ea-828d-8f16616c1c5b.jpg)


Creating deployments inside EKS cluster:

![10](https://user-images.githubusercontent.com/45136716/87224126-494a2100-c3a0-11ea-8a4d-cb573e80b2fc.jpg)

Although we can use the script to setup the deployments:-

[two.yml](https://github.com/ManthanChoudhury/amazonEKS/files/4906767/two.yml)


![11](https://user-images.githubusercontent.com/45136716/87224330-23258080-c3a2-11ea-90e3-dca3f9fd2969.jpg)

![12](https://user-images.githubusercontent.com/45136716/87224331-2456ad80-c3a2-11ea-90e6-12bbb31e4f9f.jpg)

We scaled our deployment for 3 replicas. One interesting thing to know is that kubernetes would create these pods on different node groups:-

![13](https://user-images.githubusercontent.com/45136716/87224332-26207100-c3a2-11ea-8410-f743bae417f2.jpg)

Also, for exposing the deloyments AWS provide the service for ELB (Elastic Load Balancer). It helps to manage the traffic on our website.

![14](https://user-images.githubusercontent.com/45136716/87224333-27519e00-c3a2-11ea-94aa-c03b3736341c.jpg)

Elastic Load Balancer will connect the client to different pods for managing traffic.

![15](https://user-images.githubusercontent.com/45136716/87224335-2882cb00-c3a2-11ea-933f-9b00a92dcafe.jpg)

Also for creating a persistent storage, AWS provides EBS by default. AWS has a storage class to provide PVC. Although, we can change as per our requirements.

![16](https://user-images.githubusercontent.com/45136716/87224337-291b6180-c3a2-11ea-9534-cfd9968d3bed.jpg)

![17](https://user-images.githubusercontent.com/45136716/87224339-2a4c8e80-c3a2-11ea-952f-d7e168778a8d.jpg)

HELM -- Helm helps you manage Kubernetes applications. Helm Charts help you define, install, and upgrade even the most complex Kubernetes application. HELM is similar to docker hub. It provides the charts for creating deployments.
We need to setup Kubernetes Helm in same environment as of kubectl. For installing helm refer to :- https://github.com/helm/charts


![18](https://user-images.githubusercontent.com/45136716/87224341-2c165200-c3a2-11ea-9bbc-3d9ce0b6a937.jpg)

I am creating a Jenkins deployment using helm charts.
![19](https://user-images.githubusercontent.com/45136716/87224342-2caee880-c3a2-11ea-885e-3827b3621044.jpg)

Jenkins is being setup up as a deployment and running on 8080 port. We can connect to our Jenkins cluster using browser. First we need to port forward our jenkins application using the following command:-
![20](https://user-images.githubusercontent.com/45136716/87224347-2de01580-c3a2-11ea-9187-2ff8ba6c5f06.jpg)

## How to setup the Fargate cluster in EKS?
![21](https://user-images.githubusercontent.com/45136716/87224351-2e78ac00-c3a2-11ea-8e4e-520852ca51ea.jpg)

