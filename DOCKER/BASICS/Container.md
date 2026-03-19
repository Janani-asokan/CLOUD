
* **Evolution from Physical Servers to VMs:** The video explains that physical servers often waste resources because applications rarely use 100% of the CPU and RAM. Virtual Machines (VMs) improved this by using a hypervisor to create multiple isolated logical servers on one physical machine, though they still incur overhead by requiring a full operating system for each instance 
* **The Container Advantage:** Containers are presented as an advancement over VMs. Unlike VMs, containers do not include a full operating system; they share the host’s kernel and only package the application, its libraries, and system dependencies. This makes them significantly more lightweight (often MBs vs GBs) and easier to ship across environments
* ### 2. Containers
**Containers** are an evolution of VMs designed to be even more efficient.
* **How they work:** Instead of each container having its own full OS, they all **share the host's Operating System kernel**. 
* **Benefits:** Because they only package the application and its specific requirements (libraries/dependencies), they are incredibly lightweight, start instantly, and are easy to move between different environments.
    * **Deployment Models:** Containers can be run directly on physical servers (Model 1) or on top of virtual machines (Model 2). Most modern organizations prefer Model 2 (e.g., running Docker on AWS EC2) because it reduces the maintenance overhead associated with managing physical hardware
* **Docker Life Cycle:** The instructor outlines the standard Docker workflow: writing a **Docker file** (a script of instructions), using the `docker build` command to create a **Docker image**, and finally using `docker run` to turn that image into a running **container** 
* **Introduction to Buildah:** While Docker is popular, the video introduces **Buildah** as an alternative to solve issues like "Single Point of Failure" (where all containers stop if the Docker engine fails). Buildah allows for creating images using shell scripts instead of Dockerfiles and works efficiently with tools like Podman and Skopeo 







### 1. Virtualization & Virtual Machines (VMs)
Think of a **Virtual Machine** as a "computer within a computer." 
* **The Problem:** In the past, companies ran one application per physical server, wasting a lot of hardware power.
* **The Solution:** A **Hypervisor** allows you to split one physical server into multiple VMs. Each VM has its own full Operating System (OS), making them very secure and isolated, but also "heavy" (taking up GBs of space).



### 3. Docker
**Docker** is the most popular platform used to create, deploy, and manage containers. It simplified the process through a standard "Life Cycle":
* **Docker File:** A text script containing all the commands to build an environment.
* **Docker Image:** A read-only "snapshot" or template created from the Docker File.
* **Docker Container:** A live, running instance of an image.

### 4. Buildah
**Buildah** is a tool used for building "OCI" (Open Container Initiative) compliant images. 
* **Why use it?** Unlike Docker, which requires a "Docker Engine" (a background process) to be running to build images, Buildah is **daemon-less**. 
* **The Benefit:** It reduces the "Single Point of Failure" risk—if a Docker engine crashes, everything stops. Buildah allows you to build images more flexibly, often using simple shell scripts.

---


