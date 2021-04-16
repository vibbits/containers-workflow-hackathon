# Containers

The concept of containers is not new, however is getting more attention within the Life Sciences researchers community. With the complexity of environments and conflicting dependencies in shared infrastructures (HPC clusters & cloud computing), containerization of software and tools is the appropriate solution. This tutorial and set of exercises will guide you through your first steps on how to use existing containers that are available on registries while highlighting some of the technical complexities that are often overlooked. 

## Content


```{toctree}

exercises
solutions

```

## Learner's profiles
- Who are they?
    - Researchers who wants to reuse others analysis / pipeline / software which has been containerised. 
    - Researchers that want to work more reproducibly 
    - Researchers realising that others cannot reproduce their analysis (installation, dependencies, testing, etc.)
    - Researchers that want to use other's software and need to tweak existing container recipes

       
- What challenges are they facing?
    - Hard to understand the concept of Docker and Conda environments
    - How to use and run containers, how to troubleshoot issues when running them.
    - Develop Docker images locally
    - Use singularity for deployment on HPC clusters in a command-line setting

    
- How will the lesson/workshop help them?
    - Being able to run a basic container from a container registry
    - Create an isolated environment and share a container images
    - Understand docker recipes and their documentation
    - Understand that containers do not solve the problem of correctness of analyses

## Learner's objectives

- Prerequisites for the course/tutorial
    - Experience in CLI/Linux, feeling comfortable moving around in the Terminal
    - Understand concepts of *system admin* and *installations* in the above mentioned environments

- Define exercises with learning outcomes (measurable)*
    - Use the command-line to run a bioinformatics tool/software on the command-line
    - Tweak and understand containers related parameters and how they affect the process 
    - Connect to a container and (non-)interactively run commands inside them
    - Extract information from images and containers
    - Overwrite and interact with the default working directory 
    - Bind mount a host directory to a container (use data from host directory inside a container)

*Goals: “After following one of these tutorials, learners will be able to …” - Blooms taxonomy:



