### Course Agenda

- [x] Docker Fundamentals
- [x] Docker Commands
- [ ] Docker Networking
- [ ] Docker Storage
- [ ] Docker Security
- [ ] Orchestration using Docker Swarm
- [ ] Orchestration using Kubernetes




### Keywords
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

````

### Docker CLI
````
Docker run      --> Working with Single Container
Docker Compose  --> Work with Multiple containers in a single workflow
Docker Service  --> Work with Containers in a Multi-host environment
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
            - ECR
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


````

### Dockerfile
````
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

### Assignments

**9-Oct-2021**
````
LMS - 2.8 (Images and Containers)
````

**16-Oct-2021**
````
1. 3.24 (Inspect, Remove, and Prune an Image)
2. 3.25 (Pull and Delete an Image)
````

### References
- https://docs.docker.com/get-started/overview/
- https://www.docker.com/products/docker-desktop
- https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go
















