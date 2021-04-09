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

````{admonition} Exercises
:class: note

3.1 Run a docker container and approach it interactively. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`.  


```{warning}
Don't mount a directory that contains a lot of files or subdirectories (like `~`)
``` 

3.2 Who is the default user within the container?  
 - Type `whoami`. This will give you `root`. 

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

3.6 Execute a docker container by using the `-u` option and creating a temporary file `file3.txt` with `touch`. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`
Check the file permissions of this file in the container.  


````

## 4. Using working directories 

````{admonition} Exercises
:class: note

4.1 Execute a docker container by using the working directory option `-w` for a directory `/workdir` and creating a temporary file `file4.txt` with `touch`. In addition, mount your current directory to `/workdir` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file location of this file in the container.


````

````{admonition} Exercises
:class: note

4.2 Execute a docker container and creating a temporary file `file5.txt` with `touch`. In addition, mount your current directory to `/workdir` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file location of this file in the container.


````

````{admonition} Exercises
:class: note

4.3 Use the command `docker inspect` on the current image `quay.io/biocontainers/fastqc:0.11.9--0` and extract the working directory (`WorkingDir`) using `grep`.


````


````{admonition} Exercises
:class: note

4.4 Execute a docker container with your user and group ID running `fastqc` on the file `WTXXX.fq.gz`. In addition, mount your current directory to the default working directory within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Verify that the HTML report is created with the correct file permissions.



````


````{admonition} Exercises
:class: note

4.5 Go to [Biocontainers.pro](https://biocontainers.pro/) and find the Docker image of `trimmomatic`. In addition, mount your current directory to the default working directory within the Docker container of `trimmomatic`. Verify that the HTML report is created with the correct file permissions.

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


