# Solutions




**2. Download the data**

The example fastq file(s) can be downloaded with the following commands.

```sh
wget https://introduction-containers.s3.eu-central-1.amazonaws.com/ecoli_reads.tar.gz
tar -xzvf ecoli_reads.tar.gz
```

**3. Manage file ownership while bind mounting a local directory**

````{admonition} Exercises
:class: note

3.1 Run a docker container and approach it interactively. In addition, mount the directory containing the data to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`.  
 - `docker run --rm -it -v $(pwd)/data/:/data quay.io/biocontainers/fastqc:0.11.9--0 /bin/bash`

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
 - Type `touch file1.txt`.   
 - On Mac OS, this will give you on the <your user name> and group staff.   
 - On Linux, this will give you a file with root:root permissions.

````

````{admonition} Exercises
:class: note

3.4 On the host, create a temporary file `file2.txt` in the current directory. Create a docker container and approach it interactively. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file permissions of this file in the container.  
 - Type `touch file2.txt` on the host.   
 - In the container, this will give you on e.g. 1004:1004.  
The file will appear to have user ID (UID) and group ID (GID) numbers from the user that created this in the host. If these UID and GID do exist in the container, they may have a name instead.
    
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

 - Running `id -u` will give you the effective user number, and `id -g` of the effective group number. 

`````

````{admonition} Exercises
:class: note

3.6 Execute a docker container by using the `-u` option and in the meantime creating a temporary file `file3.txt` with `touch`. In addition, mount your current directory to `/data` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`
Check the file permissions of this file in the container.  

 - By using this command line, enter your UID and GID 
`docker run --rm -u <your UID>:<your GID> quay.io/biocontainers/fastqc:0.11.9--0 touch file3.txt`

 - Especially, on your Linux host, verify the file permissions of the file `file3.txt`.

````

**4. Using working directories**

````{admonition} Exercises
:class: note

4.1 Execute a docker container by using the working directory option `-w` for a directory `/workdir` and creating a temporary file `file4.txt` with `touch`. In addition, mount your current directory to `/workdir` within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Check the file location of this file in the container.

 - `docker run --rm -v $(pwd):/workdir -w /workdir -u 1000:1000 quay.io/biocontainers/fastqc:0.11.9--0 touch file4.txt`

````


````{admonition} Exercises
:class: note

4.2 Use the command `docker inspect` on the current image `quay.io/biocontainers/fastqc:0.11.9--0` and extract the working directory (`WorkingDir`) using `grep`.

 - `docker inspect quay.io/biocontainers/fastqc:0.11.9--0 | grep 'WorkingDir'`
````


````{admonition} Exercises
:class: note

4.3 Execute a docker container with your user and group ID running `fastqc` on the file `WTXXX.fq.gz`. In addition, mount your current directory to the default working directory within the Docker container `quay.io/biocontainers/fastqc:0.11.9--0`. Verify that the HTML report is created with the correct file permissions.

```sh
# Solution
docker run \
--rm \
-u "$(id -u):$(id -g)" \
-w /data
-v $(pwd)/data/:/data
quay.io/biocontainers/fastqc:0.11.9--0 \
fastqc WT1.fq.gz
```
Or instead of `-v`/`--volume`, use `--mount`:
```
--mount type=bind,source=$(pwd)/data/,target=/data \
```
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


```sh
# Solution
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

With the example data from this exercise, this results in the following command:
```
docker run \
--rm \
-u="$(id -u):$(id -g)" \
--mount type=bind,source=$(pwd)/data/,target=/data \
quay.io/biocontainers/trimmomatic:0.35--6 \
trimmomatic \
SE \
-threads 1 \
-phred33 \
data/ecoli_1.fastq.gz \
data/ecoli_1_trimmed.fastq.gz  \
ILLUMINACLIP:$ADAPTERS:2:30:10 \
SLIDINGWINDOW:4:5 \
LEADING:5 \
TRAILING:5 \
MINLEN:25

```

````


