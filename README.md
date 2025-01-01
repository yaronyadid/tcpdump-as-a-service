
# TaaS - TCPDUMP as a Service: Empowering Regular Kubernetes Users to Capture Network Traffic

This repository demonstrates how I leveraged [Dumpy](https://github.com/larryTheSlap/dumpy) to enable regular Kubernetes users to capture network traffic (tcpdump) on their pods without requiring elevated permissions. By running privileged containers on the same node as the target pods, Dumpy provides a secure and practical solution for debugging network issues.

## What is Dumpy?

From the [Dumpy GitHub project](https://github.com/larryTheSlap/dumpy):

> Dumpy is an advanced kubectl plugin designed for Kubernetes administrators, providing seamless network traffic capture using tcpdump from various resources. It excels in isolating captures to specific pod containers or nodes, ensuring security and accurate analysis. Dumpy dynamically creates dedicated sniffers that run tcpdump for each target.

## Features

- **Network Traffic Debugging**: Allows regular users to capture traffic from pod network namespaces.
- **Minimal Permissions**: No elevated privileges are required for users.
- **Kubernetes-Native**: Utilizes RBAC, namespaces, and Security Context Constraints (SCCs).
- **Secure Implementation**: Privileged containers are isolated and managed carefully.

## Motivation

As a cluster administrator, a very common request from customers involves using tcpdump to troubleshoot application issues. Unfortunately, many customers lack the necessary permissions to run network packet captures or monitor traffic themselves, which often delays the troubleshooting process. 

Cluster administrators are often burdened with the task of manually gathering this data, consuming valuable time that could be spent on more critical administrative tasks. **TCPDUMP as a Service** automates the collection of tcpdump data, enabling quick access to critical information without requiring elevated permissions from customers, while freeing up cluster admins to focus on more impactful activities.

## How It Works

1. A privileged container runs on the same node as the target pod.
2. The container enters the network namespace of the target pod.
3. The container runs tcpdump to capture network traffic.

## How to Run It

### Using OpenShift Console (as a Regular User)

1. Go to the Developer view.
2. Click the **+Add** button.
3. Under **Developer Catalog**, go to **All Services**.
4. Select **TCPDUMP as a Service** and click **Instantiate Template**.

### Using the CLI

1. Install the tool.
2. Run the following command:

```bash
oc process tcpdump-as-a-service -n openshift -p target_pod=<pod name> -p node_name=<node name> -p params="tcpdump parameters (default: -i any)" | oc apply -f -
```

## Prerequisites

- OpenShift cluster (4.12 or higher).
- `oc` CLI tool installed.
- Permissions to create namespaces, service accounts, and assign SCCs (Cluster Admin required).

## Benefits

- **Empowers Developers**: Enables non-admin users to debug network issues independently.
- **Secure by Design**: Maintains strict control over privileged access.
- **Kubernetes-Native Workflow**: Seamlessly integrates with existing Kubernetes infrastructure.

## Failsafe

To manage resource usage effectively, I implemented a pod quota to limit the number of tcpdump pods. Since tcpdump is resource-intensive, it can overload the system's networking stack and interfere with node performance, affecting other workloads. By configuring a **ResourceQuota** in the namespace where these pods run, I ensured that tcpdump pods do not exceed the cluster's capacity or disrupt critical workloads. This safeguard maintains cluster stability while enabling essential debugging and monitoring activities without compromising system performance.

## Collaborations and Contributing

Contributions to this project are welcome! Whether you have ideas for new features, improvements, or bug fixes, your input is valuable. Here’s how you can contribute:

1. **Fork the Repository**: Click the "Fork" button at the top of the page to create a personal copy of this repository.
2. **Create a Branch**: For any changes you plan to make, create a new branch.
3. **Submit a Pull Request**: Once your changes are ready, submit a pull request with a detailed explanation of what you have done.



## Acknowledgments

This project is based on [Dumpy](https://github.com/larryTheSlap/dumpy), created by LarryTheSlap and Royce Miller. Thank you for your amazing work!


## linkedin profile - http://linkedin.com/in/yaron-yadid