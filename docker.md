### Course Agenda

- [x] Docker Fundamentals
- [ ] Docker Commands
- [ ] Docker Networking
- [ ] Docker Storage
- [ ] Docker Security
- [ ] Orchestration




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
**Assignment 1**

````
LMS - 2.8 (Images and Containers)
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
docker attach <containerid>
Exiting the container
    - type 'exit' --> come out of the container and stop it
    - CTRL+P+Q    --> Come out of the container without stopping it
docker stop <containerid>
docker start <containerid>
````

### References
- https://docs.docker.com/get-started/overview/
- https://www.docker.com/products/docker-desktop
- https://github.com/moby/moby/blob/master/pkg/namesgenerator/names-generator.go
















