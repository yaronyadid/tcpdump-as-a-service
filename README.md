TaaS - TCPDUMP as a Service: Empowering Regular Kubernetes Users to Run tcpdump

This repository demonstrates how I leveraged [Dumpy](https://github.com/larryTheSlap/dumpy) to enable regular Kubernetes users to capture network traffic (tcpdump) on their pods without requiring elevated permissions. By running privileged containers on the same node as target pods, Dumpy provides a secure and practical solution for debugging network issues.


## Whats Dumpy?
* from the Dumpy github project:
Dumpy is an advanced kubectl plugin designed for Kubernetes administrators, providing seamless network traffic capture using tcpdump from various resources. It excels in isolating captures to specific pod containers or nodes, ensuring security and accurate analysis. Dumpy dynamically creates dedicated sniffers that run tcpdump for each target.

## Features

Network Traffic Debugging: Allows regular users to capture traffic from pod network namespaces.

Minimal Permissions: Users do not require elevated privileges.

Kubernetes-Native: Uses RBAC, namespaces, and Security Context Constraints (SCCs).

Secure Implementation: Privileged container is isolated and managed carefully.

## Motivation

 As a cluster admin,A very common request from customers involves using tcpdump to troubleshoot application issues. 
 Unfortunately, many customers lack the necessary permissions to run network packet captures or monitor traffic themselves, which often delays the troubleshooting process. 
 Additionally, cluster administrators are often burdened with the task of manually gathering this data, which consumes valuable time that could be spent on more critical administrative tasks. 
 TCPDUMP as a Service provides a solution by automating the collection of tcpdump data, enabling quick access to critical information without requiring elevated permissions from customers, while freeing up cluster admins to focus on more impactful activities.



## How It Works

1. A privileged container runs on the same node as the target pod.

2. The container enters the network namespace of the target pod.

3. The container runs tcpdump to capture network traffic.

## 

## Prerequisites

Openshift cluster (4.12 or higher).

oc CLI tool installed.

Permissions to create namespaces, service accounts, and assign SCCs ( cluster admin )


## Benefits

Empowers Developers: Enables non-admin users to debug network issues independently.

Secure by Design: Maintains strict control over privileged access.

Kubernetes-Native Workflow: Seamlessly integrates with existing Kubernetes infrastructure.


## Acknowledgments

This project is based on [Dumpy](https://github.com/larryTheSlap/dumpy), created by larryTheSlap,Royce Miller Thank you for your amazing work!


## linkedin profile - http://linkedin.com/in/yaron-yadid