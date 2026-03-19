

**Key Points from the Video:**


 Virtual Machines Recap: Explains virtual machines (VMs) as a logical separation on physical servers, each with its own OS, providing security and resource isolation. VMs helped optimize physical server usage but still often waste resources.

Limitations of VMs: Even with VMs, resources are underutilized. For example, a VM allocated 25GB RAM might only use 10GB at peak, wasting the rest. This inefficiency is costly, especially at scale.

-  Introduction to Containers: Containers solve VM inefficiencies by sharing the host OS, making them lightweight. They package applications with only necessary libraries and dependencies, not a full OS, reducing overhead and improving resource usage.

-  Container Architecture: Containers can run on physical servers or VMs. They are lightweight because they share the host OS kernel and system libraries, unlike VMs which require a full OS per instance.

   docker Basics: Docker is a popular containerization platform. It uses a Dockerfile to build images, which are then run as containers. Docker’s lifecycle: Dockerfile → Docker image → Docker container.

Docker Engine: Docker Engine is central to creating and managing containers. Commands like `docker build` and `docker run` are used to create images and containers, respectively.

 Docker’s Limitations: Docker Engine is a single point of failure. If it goes down, all containers stop. Docker images also create many layers, consuming disk space.

 Buildah Introduction: Buildah addresses Docker’s limitations—no single point of failure, fewer layers, and better integration with modern tools like Podman and Kubernetes. Buildah uses shell scripts for building images, supporting Docker and OCI-compliant formats.

---

  The session introduces **containers** as part of a DevOps course, focusing on building strong fundamentals before moving to tools like Docker and Buildah.


  Explains **virtual machines (VMs)**: created using hypervisors to efficiently utilize physical servers by running multiple isolated OS environments on one machine.


  Highlights a key problem with VMs: **resource underutilization** (CPU/RAM often wasted), especially in large-scale systems like cloud instances → leads to higher costs.


  **Containers emerged as an improvement over VMs**, optimizing resource usage while still providing isolation (though less secure than full VMs).


  Describes **container architecture**:

  * Can run on physical servers or VMs
  * Modern trend favors cloud + VMs due to lower maintenance overhead


  Key concept: **Containers are lightweight** because they **don’t include a full OS**—they share the host OS and only package application + dependencies.

  A container = **application + libraries + dependencies**, making it portable and easy to transfer (smaller size vs VM images).


  Introduces **Docker workflow**:

  * Write Dockerfile → build image → run container
  * Managed via Docker Engine using commands like `docker build` and `docker run`


  Discusses **limitations of Docker**:

  * Single Point of Failure (Docker Engine)
  * Layered image inefficiencies
    → Leads to alternative tools like **Buildah**


  **Buildah** is introduced as a modern tool that solves Docker limitations and integrates well with tools like Podman and Skopeo.

---


* Containers improve **resource utilization and consistency across environments**, making deployments more efficient and predictable ([Glasp][1])
* They package applications with dependencies, ensuring **portability across systems** ([Glasp][2])


