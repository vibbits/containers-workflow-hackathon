# Containers materials
Contributors: Alexander Botzki, Marko Vidak, Mateusz Kuzak, Geert van Geest, Pedro Fernandes

## Persona 1

### Learner's profiles
- Who are they?
    - Researcher / RSE who wants to reuse others analysis / pipeline / software which has been containerised. 
    - people that have recently discovered that they have to work more reproducibly (aiming at automation, mass processing)
    - people realise that others cannot reproduce their analysis (installation, dependencies, testing, example)
    - Tweak existing container recipes
<!--    
    - mybinder / Jupyter / docker file
    - go from images to dockers
    - people have heard of it and what to use it because they want to use pipeline
    - people who want to reuse others’ software which have been containerized. 
--> 
 


       
- What challenges are they facing?
    - Hard to understand the concept of docker vs conda environments
    - They don’t know how to use or run containers, how to troubleshoot issues with running them.
    - They need to develop Docker images locally
    - Use singularity for deployment - HPC - command line / production pipeline
<!--
    - The incomplete documentation of containers they would like to use.
    - aiming at automation for mass processing
-->
    
- How will the lesson/workshop help them?
    - Being able to run a basic container from a registry
    - Understand that containers do not solve the problem of correctness of analyses
    - Create isolated environment / share image after tinkering a live images
    - Understand documentation of docker recipes

### Learner's objectives

- Prerequisites for the course/tutorial
    - basic command line experience
    - Understand concepts of ‘system admin, installation’, depending on the background

- Define exercises with learning outcomes (measurable)*
    - check whether docker is properly setup (docker run hello-world)
    - Participants are able to check whether their environment is running
    - running a container with docker run, outcomes:
    - Participant can run a container from dockerhub
    - tagging 
    - run a command
    - process listing 
    - pruning/cleaning
    - attached + interactive mode (-it)
    - detached mode 
    - running web services, mapping ports
    - volumes, bind-mounts
    - parameters (working dir, user)
    - dockerfiles
    - handling permissions
    
*Goals: “After following one of these tutorials, learners will be able to …” - Blooms taxonomy:

### Training materials
Outline: 

- intermediate example, not covered by the Carpentries lesson: running a Jupyter notebook 

- Find a image from docker hub containing bwa 
(ex: https://hub.docker.com/r/biocontainers/bwa)
- Exercise: Align reads in file `x.fastq.gz` to reference genome `y.fa` using this container with the latest BWA version from dockerhub, write the alignments to `aln-pe.sam` file: `bwa mem ref.fa read1.fq read2.fq > aln-pe.sam`


- in analogy :
	`docker run --rm --name fastqc_albot -u="$(id -u):$(id -g)" -w="/data/" -v  ~/workshop-janssen/data/:/data quay.io/biocontainers/fastqc:0.11.9--0 /bin/bash -c "fastqc WT*.fq.gz" `
    


## Persona 2

- Who are they?
    - Researcher / RSE who wants to make their analysis / pipeline / software more reusable and reproducible.
    - People that want to create Docker containers or Singularity images

- What challenges are they facing?
    - They have challenges to understand containers conceptually.
    - Current documentation from Docker/Singularity is not for beginners 
- How will the lesson/workshop help them?
    - Make sure their documentation is clear and complete.  
    - Give a template on which they can build further

### Learner's objectives
- Prerequisites for the course/tutorial
    - knowledge on command line in UNIX
    - know how to change permission/ working directory
    - package managers
    - use git 
    - account on docker hub
    - understanding a Python script
- Define exercises with learning outcomes (measurable)*
    - fetch script from git repo
    - write a Dockerfile which will create an image with a specific version of [tool] build from source with resolved dependencies, other can run this as command line tool with the parameters provided on CLI
    - put it on Docker Hub
    - requires specific python dependencies
    - default command and entrypoint


*Goals: “After following one of these tutorials, learners will be able to …” - Blooms taxonomy:


### Training materials
Use [Carpentries Docker lesson](https://carpentries-incubator.github.io/docker-introduction/) as a starting point


```sh
docker run \
--rm \
--name fastqc0119 \
-u="$(id -u):$(id -g)" \
-w="/data/" \
--mount type=bind,source=~/workshop-janssen/data/,target=/data \
quay.io/biocontainers/fastqc:0.11.9--0 \
fastqc WT1.fq.gz
```
Outline: executing bioinformatics tool on local file

- exercise
    - download example files from s3 or anywhere else
    - specific to Linux / MacOS behaves differently
    - `docker run --rm -u="$(id -u)" quay.io/biocontainers/fastqc:0.11.9--0 touch examplefile`
    - default owner of Linux is 'root'
    - explain user and group ID
    - see [Geert's course](https://sib-swiss.github.io/containers-introduction-training/course_material/managing_docker/#mounting-a-directory)
    - introduce user option 
    - `docker run --rm -u="$(id -u)" quay.io/biocontainers/fastqc:0.11.9--0 touch file1`
    - `docker run --rm -u="$(id -u):$(id -g)" quay.io/biocontainers/fastqc:0.11.9--0 touch file2`
    - learn how to know where the working directory of the image is
    - default is '/'
    - `docker inspect quay.io/biocontainers/fastqc:0.11.9--0 | grep 'WorkingDir'`
    - or `docker run --rm -it quay.io/biocontainers/fastqc:0.11.9--0`
    - ` inside the container: pwd'`
    - https://docs.docker.com/engine/reference/run
    - comment on entrypoint/cmd 
    - introduce working directory option -w 
    - we recommand to use full command e.g. `fastqc W1.fq.qz`


Outline: executing bioinformatics tool on local files

- Dockerfile: alpine, bwa, resolve dependencies, ...
- two person exercise:
    - image on docker hub 
    - produce a visualisation which is exported to png
    - write a Dockerfile which will create an image with a specific version of [tool] build from source with resolved dependencies, other can run this as command line tool with the parameters provided on CLI
    - put it on Docker Hub
    - requires specific python dependencies
    - default command and entrypoint






Outline: containerize something, container Dockerfile

- exercises 
    - fetch script from git repo
    - write a Dockerfile which will create an image with a specific version of [tool] build from source with resolved dependencies, other can run this as command line tool with the parameters provided on CLI
    - put it on Docker Hub
    - requires specific python dependencies
    - default command and entrypoint
- Dockerfile: alpine, bwa, resolve dependencies, ...
- two person exercise:
    - image on docker hub 
    - produce a visualisation which is exported to png

## Notes
- need a short section on other container registries: biocontainers, quay.io (supports podman and rkt) etc. Also to mention [open containers initiative](https://opencontainers.org/)

- Discussion about reproducibility, tagging and export of images.

## Contribution notes
This Markdown-file can be collaboratively and simultaneously edited from [this link](https://hackmd.io/@tmuylder/H1CSvMFZ_/edit).  

Please push to the branch `containers` in order not to make conflicting versions. This is automatically done when you push the Hackmd-file to GitHub (click on Settings... right top --> Versions and GitHub Sync --> Push). However, might only be done by @tmuylder. 

