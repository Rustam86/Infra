# Dependencies management

## Theory

Q: *What is Docker, and how it differs from dependencies management systems? From virtual machines?*

A: *Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.*

| Differences  | Docker  |  Virtual Machine |
|---|---|---|
| Operating system  | Docker is a container-based model where containers are software packages used for executing an application on any operating system. In Docker, the containers share the host OS kernel. Here, multiple workloads can run on a single OS  | It is not a container-based model; they use user space along with the kernel space of an OS. It does not share the host kernel. Each workload needs a complete OS or hypervisor   |
| Performance  | Docker containers result in high-performance as they use the same operating system with no additional software (like hypervisor). Docker containers can start up quickly and result in less boot-up time  |  Since VM uses a separate OS; it causes more resources to be used. Virtual machines don’t start quickly and lead to poor performance |
|  Portability | With docker containers, users can create an application and store it into a container image. Then, he/she can run it across any host environment. Docker container is smaller than VMs, because of which the process of transferring files on the host’s filesystem is easier  |  It has known portability issues. VMs don’t have a central hub and it requires more memory space to store data. While transferring files, VMs should have a copy of the OS and its dependencies because of which image size is increased and becomes a tedious process to share data |
|  Speed |  The application in Docker containers starts with no delay since the OS is already up and running. These containers were basically designed to save time in the deployment process of an application |  It takes a much longer time than it takes for a container to run applications. To deploy a single application, Virtual Machines need to start the entire OS, which would cause a full boot process |

Q: *What are the advantages and disadvantages of using containers over other approaches?*

A: 

*Advantages:*

- Consistency
> Utilizing a platform that works the same way across multiple environments eliminates so much stress. Your entire team is working in the same way, regardless of the server, machine or operating system they are using. There’s no back-and-forth between staff working through platform issues; simply create images that will transform into containers when deployed – on any device.
- Automation
> There are so many tasks that, as a developer, can become repetitive and monotonous when done manually. Docker containers allow you to schedule a range of tasks to occur when they are needed, without manual intervention from a human being. This saves time, effort, and lightens the workload for developers.
- Stability
> Docker is based on Linux and, as such, has the Linux kernel in every container, regardless of the system it is running on. In the past, this may have caused some minor stability issues when running the containers on Mac or Windows systems. These days, even though Docker updates frequently (see below), the environment remains stable on any system or device. There’s no need to suddenly roll-back to an earlier update or panic because of unforeseen compatibility issues.
- Saves Space
> The precursor to containers was the Virtual Machine (VM). VMs work in a similar way to containers, but take physical servers and spit them into virtual environments, using vast amounts of physical server space and tons of memory. Docker containers only use the code for the app and its dependencies and can run entirely on the Cloud, meaning they are much smaller and negate the requirement for large, physical servers.

*Disadvantages:*

- Advances Quickly
> This sounds like a good thing, right? Well, for the most part, it is. Docker is improving all the time, making app development and deployment slicker and more efficient. Why this is sometimes a problem is because the associated documentation doesn’t always update quite as quickly as the technology itself. This can leave developers hunting for information on certain specifics, particularly within the abstract layers when using Mac or Windows.
- Learning Curve
> Some developers find that switching to Docker containers can have quite a steep learning curve. Even those that are thoroughly familiar with VM infrastructure can find some of the Docker concepts challenging to get to grips with. That’s why working with a user-friendly container-based tool can be the key to making the most out of the Docker environment.

Q: *Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?*

A: *The Docker Engine is the underlying technology that handles the tasks and workflows involved in building container-based applications. The engine creates a server-side daemon process that hosts images, containers, networks and storage volumes. The daemon also provides a client-side command-line interface (CLI) for users to interact with the daemon through the Docker application programming interface. Containers created by Docker are called Dockerfiles. Docker Compose files define the composition of components in a Docker container.

Q: *Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).*

A: 
- *LXC (Linux)*
> LXC is a set of low-level container management tools that are part of the LinuxContainers.org open-source project. The technology was a forerunner to Docker and is sponsored by Canonical, the firm behind Ubuntu.
The goal of LXC is to provide an isolated application environment that closely resembles that of a full-blown virtual machine (VM), but without the overhead of running its own kernel. LXC also follows the Unix process model, where there is no central daemon. Put simply, instead of being managed by a single, central program, each container behaves as if it’s managed by a separate program in its own right.
LXC also works differently from Docker in a number of other ways. For example, you can run more than one process in an LXC container, whereas Docker is designed for running a single process in each container. Nevertheless, Docker is better at abstracting resources and, as a result, its containers tend to be more portable than LXC counterparts.
- *Hyper-V and Windows Containers*
> When Microsoft launched Windows Server 2016, it introduced two new container technologies, both offering lightweight alternatives to full-blown Windows virtual machines (VMs). The first, Windows Containers, takes an abstraction approach that’s similar to Docker. The other is Hyper-V Containers.
Hyper-V containers are more aligned with the VM virtualization model, as each can carry its own kernel. This means they offer greater portability than traditional containers, as applications running within them don’t need to be compatible with the host system. They also afford better security as a result of increased isolation from the host operating system and other container environments. However, these benefits come with a trade-off, as Hyper-V containers carry a slightly higher infrastructure footprint than Windows and other containers that rely on a shared kernel-based system.
You can manage Hyper-V containers using either Docker or the Windows PowerShell, but each guest environment must be Windows based, although not necessarily the same version as the host operating system.
- *Podman*
> Podman is an open-source container engine, which performs much the same role as the Docker engine. It distinguishes itself because its isolation and user privilege features make Podman inherently more secure.
Equally, its command-line interface (CLI) commands are practically identical to those supported by the Docker CLI, with the exception that you’d use Podman in place of the Docker base.
Although Docker and Podman CLI commands are similar, knowing how to tell the difference between the two will help you when working with them behind the scenes. Docker follows the client/server model, using a daemon to manage all containers under its control. However, Podman, like rkt and LXC, functions without a central daemon. This can potentially improve the resilience of any given container by eliminating the possibility of a single point of failure (SPOF). In other words, if your daemon goes down, you’ll lose control over your containers. By contrast, in Podman, containers are self-sufficient, fully isolated environments, which can managed independent of one another.
Further, where Docker gives root permission to the container user by default, non-root access is standard in Podman.

Q: *What is conda? How it differs from apt, yarn, and others?*

A: *Conda is an open source package management system and environment management system that runs on Windows, macOS, Linux and z/OS. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.*

## Problem

### Anaconda

Download latest version of conda (Anaconda):
```
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
```
Install conda:
```
Anaconda3-2022.10-Linux-x86_64.sh
```
Create a new virtual environment (named HW):
```
conda create --name HW
```
To make the changes take effect, close and then re-open your terminal window.

Test that everything is OK
```
conda list
```
Conda official repository only feature a few verified packages. A vast portion of packages are installed through community led channels called conda-forge and bioconda

Add chanells:
```
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
```
Create *packs.yml* file containing package names and versions:
```
fastqc==0.11.9
STAR==2.7.10b
samtools==1.16.1
salmon==1.9.0
bedtools==2.30.0
multiqc==1.13
picard==2.18.29
```
Install packages:
```
conda install --file packs.yml
```
picard version 2.27.5 is not in conda chanells (yet?), but picard==2.18.29 is. Authors may upload (link) new version to bioconda or conda-forge. For our usage we can use older version or get latest from [Broad Institute's github](https://github.com/broadinstitute/picard)

Create environment.yml:
```
conda env export --from-history > environment.yml
```
The content of the file should look like this:
```
name: HW
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - multiqc==1.13
  - fastqc==0.11.9
  - bedtools==2.30.0
  - salmon==1.9.0
  - samtools==1.16.1
  - star==2.7.10b
  - picard
```
To test this env (make a copy) on the same machine, change **name: HW** line to something like **name: HW_test** and run:
```
conda env create -f environment.yml
```

### Docker

Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
sudo apt-get update
```
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
Add Docker’s official GPG key:
```
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
Use the following command to set up the repository:
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Update the apt package index:
```
sudo apt-get update
```
Install Docker Engine, containerd, and Docker Compose (the latest version):
```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
