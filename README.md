# Dependencies management

## Theory

**Q**: ***What is Docker, and how it differs from dependencies management systems? From virtual machines?***

A: *Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers and dependency management systems are software for identifying, resolving, and patching dependencies for other software.

*

| Differences  | Docker  |  Virtual Machine |
|---|---|---|
| Operating system  | Docker is a container-based model where containers are software packages used for executing an application on any operating system. In Docker, the containers share the host OS kernel. Here, multiple workloads can run on a single OS  | It is not a container-based model; they use user space along with the kernel space of an OS. It does not share the host kernel. Each workload needs a complete OS or hypervisor   |
| Performance  | Docker containers result in high-performance as they use the same operating system with no additional software (like hypervisor). Docker containers can start up quickly and result in less boot-up time  |  Since VM uses a separate OS; it causes more resources to be used. Virtual machines don’t start quickly and lead to poor performance |
|  Portability | With docker containers, users can create an application and store it into a container image. Then, he/she can run it across any host environment. Docker container is smaller than VMs, because of which the process of transferring files on the host’s filesystem is easier  |  It has known portability issues. VMs don’t have a central hub and it requires more memory space to store data. While transferring files, VMs should have a copy of the OS and its dependencies because of which image size is increased and becomes a tedious process to share data |
|  Speed |  The application in Docker containers starts with no delay since the OS is already up and running. These containers were basically designed to save time in the deployment process of an application |  It takes a much longer time than it takes for a container to run applications. To deploy a single application, Virtual Machines need to start the entire OS, which would cause a full boot process |

**Q**: ***What are the advantages and disadvantages of using containers over other approaches?***

A: 

*Advantages:*

- Consistency
> Utilizing a platform that works the same way across multiple environments eliminates so much stress. Your entire team is working in the same way, regardless of the server, machine or operating system they are using. There’s no back-and-forth between staff working through platform issues; simply create images that will transform into containers when deployed – on any device.
- Automation
> Docker containers allow you to schedule a range of tasks to occur when they are needed, without manual intervention from a human being. This saves time, effort, and lightens the workload for developers.
- Stability
> Docker is based on Linux and, as such, has the Linux kernel in every container, regardless of the system it is running on. In the past, this may have caused some minor stability issues when running the containers on Mac or Windows systems. These days, even though Docker updates frequently (see below), the environment remains stable on any system or device. There’s no need to suddenly roll-back to an earlier update or panic because of unforeseen compatibility issues.
- Saves Space
> The precursor to containers was the Virtual Machine (VM). VMs work in a similar way to containers, but take physical servers and spit them into virtual environments, using vast amounts of physical server space and tons of memory. Docker containers only use the code for the app and its dependencies and can run entirely on the Cloud, meaning they are much smaller and negate the requirement for large, physical servers.

*Disadvantages:*

- Advances Quickly
> Docker is improving all the time, making app development and deployment slicker and more efficient. Why this is sometimes a problem is because the associated documentation doesn’t always update quite as quickly as the technology itself. This can leave developers hunting for information on certain specifics, particularly within the abstract layers when using Mac or Windows.
- Learning Curve
> Switching to Docker containers can have quite a steep learning curve. 

**Q**: ***Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?***

A: *The Docker Engine is the underlying technology that handles the tasks and workflows involved in building container-based applications. The engine creates a server-side daemon process that hosts images, containers, networks and storage volumes. The daemon also provides a client-side command-line interface (CLI) for users to interact with the daemon through the Docker application programming interface. Containers created by Docker are called Dockerfiles. Docker Compose files define the composition of components in a Docker container.*

**Q**: ***Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).***

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

**Q**: ***What is conda? How it differs from apt, yarn, and others?***

A: *Conda is an open source package management system and environment management system that runs on Windows, macOS, Linux and z/OS. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. It was created for Python programs, but it can package and distribute software for any language.
The main difference between conda and apt, yarn, and (maybe) others is that conda provides not only dependency management, but also virtualisation, allowing to run different versions of the same software on one OS*


## Problem

### Anaconda

Download latest version of conda (Anaconda):
```
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
```
Install conda:
```
bash Anaconda3-2022.10-Linux-x86_64.sh
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
  - picard==2.18.29
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

Make a Doclerfile, containing:
```
FROM ubuntu:22.04

# Install base utilities
RUN apt-get update
RUN apt-get install build-essential -y
RUN apt-get install -y wget
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
RUN /bin/bash ~/miniconda.sh -b -p /opt/conda

# Put conda in path
ENV PATH=$CONDA_DIR/bin:$PATH

# Add conda chanells
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --set channel_priority strict

# Install packages
RUN conda install fastqc==0.11.9 STAR==2.7.10b samtools==1.16.1 salmon==1.9.0 bedtools==2.30.0 multiqc==1.13 picard==2.18.29
```

To buil an image from the Docker file run (Dockerfile is inside Bio folder):
```
sudo docker build Bio/ -t bio
```
Run bio image:
```
sudo docker run --rm -it bio
```
After using hadolint Docker image looks like this (added versions and --no-install-recommends):
```
FROM ubuntu:22.04

# Install base utilities
RUN apt-get update
RUN apt-get install --no-install-recommends build-essential=12.9ubuntu3 -y
RUN apt-get install --no-install-recommends -y wget=1.21.2-2ubuntu1
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
RUN /bin/bash ~/miniconda.sh -b -p /opt/conda

# Put conda in path
ENV PATH=$CONDA_DIR/bin:$PATH

# Add conda chanells
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --set channel_priority strict

# Install packages
RUN conda install fastqc==0.11.9 STAR==2.7.10b samtools==1.16.1 salmon==1.9.0 bedtools==2.30.0 multiqc==1.13 picard==2.18.29

```
Use to check the package version:
```
apt-cache policy PACKAGE
```

Still one warning: "Delete the apt-get lists after installing something", no idea how to fix it because all it suggests doing was already done:
```
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
```
Final version of Dockerfile with labels:
```
FROM ubuntu:22.04

# Labels
LABEL maintainer="rustam@heydarov.ru"
LABEL build_date="December 2022"
LABEL description='Tools for excellent RNA-seq analysis pipeline'
LABEL url='https://github.com/Rustam86/Infra#dependencies-management'

# Install base utilities
RUN apt-get update
RUN apt-get install build-essential=12.9ubuntu3 -y
RUN apt-get install -y wget=1.21.2-2ubuntu1
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Install miniconda
ENV CONDA_DIR /opt/conda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
RUN /bin/bash ~/miniconda.sh -b -p /opt/conda

# Put conda in path
ENV PATH=$CONDA_DIR/bin:$PATH

# Add conda chanells
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --set channel_priority strict

# Install packages
RUN conda install fastqc==0.11.9 STAR==2.7.10b samtools==1.16.1 salmon==1.9.0 bedtools==2.30.0 multiqc==1.13 picard==2.18.29
```
"--no-install-recommends" flags were removed because of "The command '/bin/sh -c wget --quiet "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" -O ~/miniconda.sh' returned a non-zero code: 5" error


Second final version of Dockerfile (you know why it here):
```
FROM ubuntu:22.04

# Labels
LABEL maintainer="rustam@heydarov.ru"
LABEL build_date="December 2022"
LABEL description='Tools for excellent RNA-seq analysis pipeline'
LABEL url='https://github.com/Rustam86/Infra#dependencies-management'

# Install base utilities
RUN apt-get update \
&& apt-get install build-essential=12.9ubuntu3 -y \
&& apt-get install -y wget=1.21.2-2ubuntu1 \
&& apt-get install unzip \
&& apt-get -y install perl \
&& apt-get -y install openjdk-11-jdk xvfb \
&& apt-get -y install python3-pip \
&& apt-get -y install libgomp1 \
&& apt-get -y install libtbb12 \
&& touch /.bashrc

# Install packages

# FastQC==0.11.9
RUN wget https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.9.zip \
&& unzip fastqc_v0.11.9.zip \
&& chmod a+x /FastQC/fastqc \
&& echo 'alias fastqc="/FastQC/fastqc"' >> /.bashrc

# STAR==2.7.10b
RUN wget https://github.com/alexdobin/STAR/releases/download/2.7.10b/STAR_2.7.10b.zip \
&& unzip ./STAR_2.7.10b.zip \
&& chmod a+x ./STAR_2.7.10b/Linux_x86_64_static/STAR \
&& mv ./STAR_2.7.10b/Linux_x86_64_static/STAR /bin/STAR \
&& rm -r ./STAR_2.7.10b

# samtools==1.16.1
RUN wget https://github.com/samtools/samtools/archive/refs/tags/1.16.1.zip -O ./samtools-1.16.1.zip \
&& unzip ./samtools-1.16.1.zip \
&& mv ./samtools-1.16.1/misc /samtools\
&& rm -r ./samtools-1.16.1 \
&& echo 'alias samtools="/samtools/samtools.pl"' >> /.bashrc

# picard==2.27.5
RUN wget https://github.com/broadinstitute/picard/releases/download/2.27.5/picard.jar -O /bin/picard.jar \
&& chmod a+x /bin/picard.jar \
&& echo 'alias picard="java -jar /bin/picard.jar"' >> /.bashrc

# bedtools==2.30.0
RUN wget https://github.com/arq5x/bedtools2/releases/download/v2.30.0/bedtools.static.binary -O /bin/bedtools.static.binary \
&& chmod a+x /bin/bedtools.static.binary\
&& echo 'alias bedtools="/bin/bedtools.static.binary"' >> /.bashrc

# MultiQC==1.13
RUN pip install multiqc==1.13

# salmon==1.9.0
RUN wget https://github.com/COMBINE-lab/salmon/releases/download/v1.9.0/salmon-1.9.0_linux_x86_64.tar.gz \
&& tar -zxvf ./salmon-1.9.0_linux_x86_64.tar.gz \
&& chmod a+x ./salmon-1.9.0_linux_x86_64/bin/salmon \
&& mv ./salmon-1.9.0_linux_x86_64/bin/salmon /bin/salmon \
&& rm -r ./salmon-1.9.0_linux_x86_64 

# Cleanup
RUN rm ./*zip \
&& rm ./*tar.gz \
&& apt-get autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*
