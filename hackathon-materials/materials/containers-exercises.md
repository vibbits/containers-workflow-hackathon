## Learning outcomes

**After having completed this chapter you will be able to:**

* Use the command line to run a bioinformatics tool on the command line
* Set the default user and group with the `-u` option
* Run a command inside a container non-interactively
* Use `docker inspect`to get more information on an image and container
* Overwrite the default working directory within a container with `-w` 
* Use the option `--mount` to bind mount a host directory to a container

## Material

[:fontawesome-solid-file-pdf: Download the presentation](../assets/pdf/managing_docker.pdf){: .md-button }

* [Overview of how docker works](https://docs.docker.com/get-started/overview/)
* [More on bind mounts](https://docs.docker.com/storage/bind-mounts/)
* [Docker volumes in general](https://docs.docker.com/storage/volumes/)

## Exercises

At the end of the exercises, you will run fastqc on one fastq file by using a docker container.

### Download the example fastq file(s)

In order to download the example file, please use the following commands:

```sh
wget https://introduction-containers.s3.eu-central-1.amazonaws.com/ecoli_reads.tar.gz
tar -xzvf ecoli_reads.tar.gz
```

### Manage file ownership while bind mounting a local directory

**Exercise:** Run a docker container and approach it interactively. In addition, mount your current directory to `/data` within the Docker container quay.io/biocontainers/fastqc:0.11.9--0 .

!!! warning
    Don't mount a directory that contains a lot of files or subdirectories (like `~`)

??? done "Answer"
    
    `docker run --rm -it -v ~/data/:/data quay.io/biocontainers/fastqc:0.11.9--0 /bin/bash`

**Exercise:** Who is the default user within the container?

??? done "Answer"
    Type `whoami`. This will give you `root`. 

    
**Exercise:** Create a temporary file `file1.txt` in the current directory in the container. On your host, check the file permissions.
Quit the interactive session.

??? done "Answer"
    Type `touch file1.txt`. 
    On Mac OS, this will give you on the <your user name> and group staff. 
    On Linux, this will give you a file with root:root permissions.


**Exercise:** On the host, create a temporary file `file2.txt` in the current directory. Create a docker container and approach it interactively. In addition, mount your current directory to `/data` within the Docker container quay.io/biocontainers/fastqc:0.11.9--0
Check the file permissions of this file in the container.

??? done "Answer"
    Type `touch file2.txt` on the host. 
    In the container, this will give you on e.g. 1004:1004.
    
    The file will appear to have user ID (UID) and group ID (GID) numbers from the user that created this in the host. If these UID and GID do exist in the container, they may have a name instead.
    
**Exercise:** On the host, find out which UID and GID you have. 

!!! hint 
    You can find your UID and GID with:
    
    ```
    id -u
    id -g
    ```

??? done "Answer"
    Running `id -u` will give you the effective user number, and `id -g` of the effective group number. 
    
**Exercise:** Execute a docker container by using the `-u` option and creating a temporary file file3.txt with `touch`. In addition, mount your current directory to `/data` within the Docker container quay.io/biocontainers/fastqc:0.11.9--0
Check the file permissions of this file in the container.


By using this command line, enter your UID and GID 
`docker run --rm -u=<your UID>:<your GID> quay.io/biocontainers/fastqc:0.11.9--0 touch file3.txt`

Especially, on your Linux host, verify the file permissions of the file `file3.txt`.

### Using working directories 

**Exercise:** Execute a docker container by using the working directory option `-w` for a directory `/workdir` and creating a temporary file file4.txt with `touch`. In addition, mount your current directory to `/workdir` within the Docker container quay.io/biocontainers/fastqc:0.11.9--0
Check the file location of this file in the container.

??? done "Answer"

    ```sh
    docker run --rm -v $(pwd):/workdir -w /workdir -u=1000:1000 biocontainers/fastqc:v0.11.9_cv7 touch file4.txt
    ```

**Exercise:** Execute a docker container and creating a temporary file file5.txt with `touch`. In addition, mount your current directory to `/workdir` within the Docker container quay.io/biocontainers/fastqc:0.11.9--0
Check the file location of this file in the container.

??? done "Answer"

    ```sh
    docker run --rm -v $(pwd):/workdir -u=1000:1000 biocontainers/fastqc:v0.11.9_cv7 touch file5.txt
    ```

**Exercise:** Use the command `docker inspect` on the current image quay.io/biocontainers/fastqc:0.11.9--0 and extract the working directory (WorkingDir) via grep.


`docker inspect quay.io/biocontainers/fastqc:0.11.9--0 | grep 'WorkingDir'`


**Exercise:** Execute a docker container with your user and group ID running `fastqc` on the file `WTXXX.fq.gz` . In addition, mount your current directory to the default working directory within the Docker container quay.io/biocontainers/fastqc:0.11.9--0
Verify that the HTML report is created with the correct file permissions.

??? done "Answer"

    ```sh
    docker run \
    --rm \
    -u="$(id -u):$(id -g)" \
    --mount type=bind,source=$(pwd)/data/,target=/data \
    quay.io/biocontainers/fastqc:0.11.9--0 \
    fastqc WT1.fq.gz
    ```


**Exercise:** Got to Biocontainers.pro and find the Docker image of trimmomatic. In addition, mount your current directory to the default working directory within the Docker container of trimmomatic
Verify that the HTML report is created with the correct file permissions.

??? done "Answer"

    ```sh
    docker run \
    --rm \
    -u="$(id -u):$(id -g)" \
    --mount type=bind,source=$(pwd)/data/,target=/data \
    quay.io/biocontainers/trimmomatic:XXXXX \
    trimmomatic \
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
    ```






