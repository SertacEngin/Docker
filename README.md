# Docker

A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one 
computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything 
needed to run an application: code, runtime, system tools, system libraries and settings. Simply, a container is a bundle of Application, Application libraries required to run your application and the minimum system dependencies.

![1](https://github.com/user-attachments/assets/b4a656ac-87d1-49e4-8134-3319ae99b027)

If we consider VMs an advanced model of servers than we can consider containers an advanced model of VMs. One problem we might have with VMs is 
that we might not use its full resources like CPU, RAM, hardware etc.. When we have 1 VM it might be fine but when we have 100s of them it is a 
big problem.

Then Hypervisor was invented. Hypervisor is some kind of virtualization. Virtualization is creating multiple VMs on our physical servers. A 
virtual server is basically a virtual separation. A virtual machine is a logical isolation that has an OS installed on it. We run our 
applications on these operating systems. Each VM has its own OS which makes it secure.
VMs are logically separated because of the operating systems that they have.

When we have VMs why would we need containerization?
By using a Hypervisor we create virtual machines on our server. The same thing happens when we create EC2 instances. But even after creating 
virtual machines we might not be using them to their full capacity.
Let’s say our VM1 runs our App1. Let’s say its capacity is 25 GB of RAM and 25 CPU. But our app is using 10 GB of RAM and 6 CPU at its full 
capacity. So the resources that we don’t use on this VM is 15 GB of RAM and 19 CPU. It might be even more resources wasted from time to time. 
This is the major drawback of VMs. 

VMs solve some problems of physical servers and containers solve some problems of VMs. The problem of wasting resources of VMs can be solved 
with containers. While VMs have their own OS, containers don’t have a complete OS. There is logical isolation for containers but this isolation 
is not complete.

Let’s take a look at the architecture of containers. Containers can be created 2 ways. First, on VMs, and second, on physical servers.
We can install Docker on the OS of our physical server and create containers with it. But there is a lot of maintenance needed here.
We can install Docker on our VMs as well. This is modern way as it requires less maintenance overhead.
Containers are quite lightweight in their nature. Containers use the resources of the OS that they are built on. Let’s say that our VM has Linux 
installed on it and we have 5 containers on this VM. All these containers use this Linux’s shared libraries and dependencies for their work.
Containers have a minimal OS (Base Image).
A container is a package which is a combination of  our application + its libraries and dependencies + system dependencies. And the container 
uses these shared resources of the VM.

Let’s say we take a snapshot of our VM and it is typically from 1 to 2 GB.
But when we take a snapshot of a container it is typically from 100 to 500 MB.
Containers are easy to ship, deploy, or transfer because of their light weight because they don’t have a complete OS and they use the resources 
of the OS on which they run on.

Let’s say we need various containers. One with python, one with node.js, one with Java etc.. In our Docker we have a base image that has all the 
system dependencies.
These system dependencies + our application + application libraries will form our Docker image (container). So we can’t say Docker images don’t 
have an operating system. But we can say that they have a minimal OS with system dependencies.

Why is Docker very popular?
Docker improves the concept of containerization. We write a dockerfile like we write a jenkins file.
And we submit file to docker engine using commands. And the docker engine converts this file into an image. Again using some docker commands we 
can convert this image into a docker container.

So the lifecycle in docker containerization is like this:
1- We write a Dockerfile.
2- We create an image to execute this docker file.
3- We execute this image to create a container.

In Docker platform there is Docker engine that is used to create Docker images and containers.
To create a docker image from a dockerfile we use the command “docker build”.
To create a container from an image we use the command “docker run”.

Docker is dependent on docker engine which is a single point of failure. If the docker engine is down for some reason, all our docker containers 
will stop working.
Buildah is used to solve this problem. Buildah works without a running Docker daemon. We can build images as a regular process, not tied to 
Docker Engine. We can use Buildah for building images on Kubernetes nodes directly (without Docker).

Buildah doesn’t replace Docker completely — it focuses on building images (not running containers). It’s great for:   
Security-conscious environments (rootless builds).
Kubernetes-focused workflows (especially OpenShift).
CI/CD pipelines where you want to avoid Docker daemon dependency.

The Docker Daemon is a background service (a process) that manages all Docker objects on your system, including containers, images, volumes, 
networks. It acts as the brains behind Docker, coordinating all the tasks related to building, running, and stopping containers. Without the 
Docker Daemon, Docker simply doesn't work.

The Docker Daemon (dockerd) is the core service that manages Docker containers, images, networks, and volumes. It acts as the backend that 
processes all Docker CLI commands. Without the Docker Daemon, Docker containers cannot run, and Docker CLI commands fail. In production, systemd 
or Kubernetes often helps monitor and restart the daemon if it crashes.

Docker Engine is the entire Docker platform that lets you build, run, and manage containers. It includes 3 main components:
Docker Daemon (dockerd): The background service that manages containers, images, networks, and volumes.
Docker CLI (docker): The command-line tool you use to talk to the Docker Daemon.
Docker API: The API that lets other tools (and the CLI itself) communicate with the Docker Daemon.

Analogy
Think of Docker Engine as a car:

Part	              Role
Docker Engine	      The whole car
Docker Daemon	      The engine (runs the car)
Docker CLI	        The steering wheel (you control the car)
Docker API	        The electronics (how systems talk to the engine)
