### Course Agenda

- [x] Docker Fundamentals
- [x] Docker Commands
- [x] Docker Networking
- [x] Orchestration using Docker Swarm
- [ ] Docker Storage
- [ ] Docker Security
- [ ] Orchestration using Kubernetes


SWMKEY-1-47S+pMHNdplgG1HhSThDkCRcubrSZ638TNxsjcVVlnQ


VXNET
iptables
SNAT/DNAT





### Keywords / Concepts
````
- Hypervisors --> Containers
- ESXi / HyperV / KVM / ---> Docker / CRI-O / RKT / Containerd / Podman
- Pluggable architecture
- Compute Evolution

Physical Machines (5-10%) ---> Virtual Machines (60-70%)  ---> Containers (90%) 
                                                          ---> Serverless (100%)
Docker != Containers
Docker vs Kubernetes
Containers ---> OS/Kernel level Virtualization (Container Runtimes)
Virtual Machines ---> Hardware level Virtualization (Hypervisor)

Image ==> OS + Middleware + dependencies + App

Private Cloud Implementation
    - Openstack  ---> Mirantis, RedHat, IBM
    - Cloud Foundry

- Docker Machine (Not to be confused with "Docker Engine")
- Docker Toolbox

Windows Laptop--> Docker Machine ---> VirtualBox --> linux VM ---> Docker

CMD vs ENTRYPOINT
COPY vs ADD

SDDC --> Software Defined Data Centres
    - Server Virtualization --> ESXi / HyperV
    - SAN - EMC2, NetAPP, IBM (AWS EBS / Azure Block)
    - SDN - VMware NSX, 

API
    - API developers
    - API consumers (DevOps / SRE)

Communication Channels:
IPC --> Inter process Communication (Monolithics)
API --> Application Programming Interface (Microservices)
VMware vMotion

````

### Docker CLI
````
Docker run      --> Working with Single Container
Docker Service  --> Work with Containers in a Multi-host environment
Docker Compose  --> Work with Multiple containers in a single workflow
Docker Stack    --> Docker Compose files in a Multi-host environment

````



### Container Runtimes
````
- Docker
- CRI-O
- RKT
- Podman
- containerd
- OCI
````
### Container Orchestration Engines (COEs)
````
=> On-Prem
  - Kubernetes
  - Docker Swarm
  - Apache Mesos
  - OpenShift

=> Cloud based
  - ECS
  - EKS
  - AKS 
  - GKE
````

### Docker Versions
````
  CE --> Community Edition
  EE --> Enterprise Edition (Mirantis Docker)
````

**Classroom Activity 1 (LMS - 2.5 and 2.6)**
````
- Installing docker
    
    - https://docs.docker.com/engine/install/ubuntu/
    - Simplilearn Lab 2.5
    - get.docker.com

- validating the installation (by running hello-world)
- Enabling Docker service
      - systemctl start docker
      - systemctl enable docker
- Add user to Docker group
    sudo su -
    usermod -aG docker <labsuser>

````

### Docker Architecture
````
    - Docker Host
    - Docker Daemon
    - Docker Client
    - Docker Container (AWS EC2 / VMs)
    - Docker Images (AWS AMI / Templates)
    - Docker registry
        - Public
            - Docker Hub (hub.docker.com)
        - Private
            - ECR (AWS --> IAM)
            - ACR
            - MSR

- Registry
    --> Repository
        --> Versions/tags    
````

**Docker Orchestration Workflow**
````
User (You) --> Swarm commands ---> Docker API ---> Docker Daemon --> host kernel
````




### Docker commands
````
docker search ---> lists the images on Docker Hub
docker image ls (docker images) --> lists the local images
docker ps (docker container ls)
docker ps -a (docker container ls -a)
docker pull nginx == docker pull nginx:latest
docker run <imagename>
docker run
      -i - interactive
      -t - terminal
      -d - detached/daemonized
      --name (-n) - give a user defined name to container

docker attach <containerid>
Exiting the container
    - type 'exit' --> come out of the container and stop it
    - CTRL+P+Q    --> Come out of the container without stopping it
docker stop <containerid>
docker start <containerid>

docker run -it
docker run --memory 500M --memory-reservation 250M

docker exec -it --> run a command inside a container without going into it
docker attach (similar to ssh into a VM)


docker diff --> verify the changes between the source image and container
docker inspect <Objectid or Objectname>

docker pull ubuntu ---> docker pull ubuntu:latest
docker pull nginx ---> docker pull nginx:latest
docker history nginx ---> docker history nginx:latest
docker imagename --> docker imagename:tag (tag defaults to 'latest')
docker image ls --> list images on Docker host
docker image rm --> remove a docker image from the host

docker tag --> rename an image or tag

docker commit --> create a new image from container

existing image ----> docker run ---> edit the container ---> commit as a new image

Port binding
Syntax:
-P --> random port of host to port 80 of container
-p hostport:guestport

Example:
docker run -P <imagename>
docker run -p 8888:80 <imagename>

Flattening an Image

Create a Container (docker run) ---> Export that container as tarball (docker export) ---> import that container into a new image (docker import)

Step 1 - Create a container:
docker run -d --name=flat-container mynginx

Step 2 - Export the container as Tarball:
docker export flat-container > flat.tar

Step 3 - Import the tarball into and image:
cat flat.tar | docker import - mynginx:flat

Step 4 - Validate the changes by checking image history:
docker history mynginx:latest
docker history mynginx:flat


````

### Dockerfile
````
FROM
RUN
CMD
ENTRYPOINT
COPY
ADD
ESXPOSE
ENV


## comment
INSTRUCTION argument

Syntax:
FROM <imagename>
RUN command
COPY 
CMD command


Example:

FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install -y nginx
COPY index.html /var/www/html
EXPOSE 80
CMD nginx -g 'daemon off;'

Build an image from Dockerfile using the following command:

Default Dockerfile in current directory:
docker image build -t custom-nginx:latest .

Customer Dockerfile in a different directory:
docker image build -t custom-nginx:latest -f /location/file .

````

### CIDR Networking

````
Network bits (Fixed) / hosts bits (variable)

10.0.0.0/8      ---> 10.{0-255}.{0-255}.{0-255} ---> 256x256x256 --> 16,777,216
172.17.0.0/16   ---> 172.17.{0-255}.{0-255} --> 256x256 ---> 65,536
172.31.1.0/24   ---> 172.31.1.{0-255} --> 256
1.2.3.4/32      ---> 1.2.3.4
0.0.0.0/0       ---> All the possible IP addresses
````

**Class Activity (Flattening images)**

````
Step 1 - Create a container:
docker run -d --name=flat-container mynginx

Step 2 - Export the container as Tarball:
docker export flat-container > flat.tar

Step 3 - Import the tarball into and image:
cat flat.tar | docker import - mynginx:flat

Step 4 - Validate the changes by checking image history:
docker history mynginx:latest
docker history mynginx:flat
````


**Multi Stage Builds**
**Part 1 (Without Multistage)**
````
Step 1 - Write a helloworld program in Go
vi helloworld.go

package main
import "fmt"
func main () {
    fmt.Println("Hello MultiStage!")
}

Step 2 - Create a Dockerfile
vi Dockerfile

FROM golang:1.12.4
WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .
CMD ["./helloworld"]

Step 3 - Build an image from the Dockerfile

docker build -t inefficient .
````
**Part 2 (With Multistage)**
````
Write Dockerfile with Multi Stage

vi Dockerfile

FROM golang:1.12.4 AS stage1

WORKDIR /helloworld
COPY helloworld.go .
RUN GOOS=linux go build -a -installsuffix cgo -o helloworld .

FROM alpine:latest
WORKDIR /root
COPY --from=stage1 /helloworld/helloworld .
CMD ["./helloworld"]

````

Containers on same host --> Bridge/host
Containers on different host --> Overlay network (SDN --> Software Defined Networking)
Kubernetes --> CNI (Flannel, Calico, Weave / VPC / )

**23-Oct-2021**

**Class Activity**
````
4.3
4.4
4.6
4.9
4.19 
````

**Sample daemon.json file**
````
vi /etc/docker/daemon.json

{
    "dns": ["8.8.8.8", "8.8.4.4"]
}
````


### #############################
### Docker Swarm
### #############################

**Swarm Terminology**
````
Runtime (Docker in our case)
Swarm
Tasks
Replicas
Manager/Leader/Worker Nodes
docker service (replacement for docker run)
````

**Class Activity**

````
5.8 - Set up Swarm Cluster with a Manager and Worker Node
5.9 - Join Nodes to Swarm

5.10 - Create Replicated and Global Services
5.11 - Running Container vs. Running Service
5.12 - Create an Overlay Network
4.17 - Publishing Ports
````
**24-Oct-2021**

**Class Activity**
````
5.13
5.14
5.15

5.17
5.19
````

**Class Activity: Docker Compose**
````
1. Docker Compose installation:
Reference: https://docs.docker.com/compose/install/

Steps:
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version


2. Working with Docker Compose
Complete the following Tutorial:

https://docs.docker.com/samples/wordpress/

````

### Assignments

**6-Oct-2021**
````
1. 2.8 (Images and Containers)
````

**7-Oct-2021**
````
1. 3.24 (Inspect, Remove, and Prune an Image)
2. 3.25 (Pull and Delete an Image)
````

**8-Oct-2021**
````
1. 3.19 Configure a registry
2. 3.20 Login to a registry
3. 3.21 Push an image to Dockerhub
4. 3.22 Push an image to registry
````

### References
- https://docs.docker.com/get-started/overview/
- https://www.docker.com/products/docker-desktop
- https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go
- https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
- https://docs.docker.com/develop/develop-images/multistage-build/
- https://docs.docker.com/develop/develop-images/baseimages/
- https://dzone.com/articles/docker-layers-explained
- https://linuxjourney.com/
- https://dzone.com/articles/docker-container-resource-management-cpu-ram-and-i
- https://docs.docker.com/engine/swarm/swarm-tutorial/
- https://github.com/swarmpit/swarmpit#installation
- https://swarmpit.io/
- https://blog.neuvector.com/article/docker-swarm-container-networking
- https://apimirror.com/docker~17/engine/swarm/swarm-tutorial/rolling-update/index
- 
























