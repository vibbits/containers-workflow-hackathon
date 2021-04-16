# Exercises
For this set of exercises we will use a simple Docker container for `fastQC` process, more specifically [quay.io/biocontainers/fastqc](https://quay.io/repository/biocontainers/fastqc?tab=info) (version 0.11.9--0). 
At the end of the exercises, you will run `fastQC` on a fastq-file by using a Docker container.


```{admonition} Learning outcomes
:class: tip

After having completed this chapter you will be able to:  
* Use the command line to run a bioinformatics tool on the command line
* Set the default user and group with the `-u` option
* Run a command inside a container non-interactively
* Use `docker inspect`to get more information on an image and container
* Overwrite the default working directory within a container with `-w` 
* Use the option `--mount` to bind mount a host directory to a container

```


## 1. Introduction Docker 
We refer to the following tutorials and documentation that will guide you through the concepts of Docker that will get you started for this set of exercises. 

* [Overview of how docker works](https://docs.docker.com/get-started/overview/)
* [More on bind mounts](https://docs.docker.com/storage/bind-mounts/)
* [Docker volumes in general](https://docs.docker.com/storage/volumes/)


## 2. Download the data

The example fastq file(s) can be downloaded with the following commands. We will use them in combination with the Docker containers to mimic a simple, though relevant bioinformatics data analysis process. 

```sh
wget https://introduction-containers.s3.eu-central-1.amazonaws.com/ecoli_reads.tar.gz
tar -xzvf ecoli_reads.tar.gz
```

## 3. Manage file ownership while bind mounting a local directory

A docker container image is run with the following command:
```
docker run <options> <image-name>:<version> [command] 
```
with `<image-name>:<version>` being `quay.io/biocontainers/fastqc:0.11.9--0`. The first time you are trying to run this command, the image is not available locally, hence it will be downloaded from its repository. 

There are a lot of available parameters that specify how the docker container is being run, to have an overview, type `docker run --help`. 

Docker containers are fully isolated. It is necessary to mount volumes in order to handle input/output files. By default, Docker containers cannot access data on the host system. This means that:
- we can’t use host data in the containers
- all data stored in the container will be lost when the container exits

This can be solved in two ways:
- `-v /path/in/host:/path/in/container`: This **bind mounts** a host file or directory into the container. Note that both paths have to be absolute paths, so you often want to use `$(pwd)`. 
- `-v volume_name:/path/in/container`. This mounts a **named volume** into the container, which will live separately from the rest of your files. This is preferred, unless you need to access or edit the files from the host.


````{note}
To have an overview of all the images locally available, use:
```
docker images
```
To have an overview of all running containers:
```
docker ps
```
We can stop and subsequently remove a running container with 
```
docker stop <container-id>
docker rm <container-id>
```
````

````{admonition} Exercises
:class: note

3.1 Run a docker container and approach it interactively. In addition, mount the directory containing the data to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`.   


```{warning}
Don't mount a directory that contains a lot of files or subdirectories (like `~`)
``` 
```` 

The following three exercises aim to give an idea of how folders and files are managed on your computer locally as opposed to our Docker containers. Try to answer the following questions and think about how the 

````{admonition} Exercises
:class: note

3.2 Who is the default user within the container?  

````


````{admonition} Exercises
:class: note

3.3 Create a temporary file `file1.txt` in the current directory in the container. On your host, check the file permissions.
Quit the interactive session.  


````

````{admonition} Exercises
:class: note

3.4 On the host, create a temporary file `file2.txt` in the current directory. Create a docker container and approach it interactively. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file permissions of this file in the container.  

    
````


`````{admonition} Exercises
:class: note

3.5 On the host, find out which UID and GID you have. 

````{hint}
You can find your UID and GID with:
    
```
id -u
id -g
```
````  


`````

````{admonition} Exercises
:class: note

3.6 Execute a docker container by using the `-u` option and and in the meantime creating a temporary file `file3.txt` with `touch`. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`
Check the file permissions of this file in the container.  

````

After these exercises it should be clear that docker containers will output files at `root`-level by default, however that we can overcome this behaviour by using the user ID and group ID levels on run-time. To generalize this command over different infrastructures (with possible different settings) we can provide it the following parameter `--user $(id -u):(id -g)`. 

## 4. Using working directories 

The *working directory* sets the location for running instructions (installations, commands, file copying, etc.) defined in the `Dockerfile`. The working directory is described in the `Dockerfile` with:
```
WORKDIR /path/to/workdir
```
As an example, have a look at the Dockerfile of our `fastqc` container [here](https://github.com/BioContainers/containers/blob/master/fastqc/0.11.9/Dockerfile). 

````{admonition} Exercises
:class: note

4.1 Execute a docker container by using the working directory option `-w` for a directory `/workdir` and creating a temporary file `file4.txt` with `touch`. In addition, mount your current directory to `/workdir` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file location of this file in the container.


````


````{admonition} Exercises
:class: note

4.2 Use the command `docker inspect` on the current image `quay.io/biocontainers/fastqc:0.11.9--0` and extract the working directory (`WorkingDir`) using `grep`.


````


````{admonition} Exercises
:class: note

4.3 Execute a docker container with your user and group ID running `fastqc` on the file `WTXXX.fq.gz`. In addition, mount your current directory to the default working directory within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Verify that the HTML report is created with the correct file permissions.

````



````{admonition} Exercises
:class: note

4.4 Go to [Biocontainers.pro](https://biocontainers.pro/) and find the Docker image of `trimmomatic`. In addition, mount your current directory to the default working directory within the Docker container of `trimmomatic`. Verify that the HTML report is created with the correct file permissions.

For this you can use the following set of parameters:

    SE \
    -threads 1 \
    -phred33 \
    input.fastq \
    output.fastq \
    ILLUMINACLIP:$ADAPTERS:2:30:10 \
    SLIDINGWINDOW:4:5 \
    LEADING:5 \
    TRAILING:5 \
    MINLEN:25




````


