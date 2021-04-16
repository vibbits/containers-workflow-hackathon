# Exercises
For this set of exercises we will use a [simple RNAseq pipeline](https://github.com/nextflow-io/rnaseq-nf) with only a few processes. 

```{admonition} Learning outcomes
:class: tip

After having completed this chapter you will be able to:  
1. Introduction nextflow and language (theoretical)
2. Knowing where to find a pipeline and which one to use.
3. Import a pipeline.
4. Execute a pipeline.
5. Locate and describe the output after running a pipeline.
6. Run a pipeline with different parameters.
7. Explain config files and being able to do minor modifications.
```

## 1. Introduction nextflow and language (theoretical)
There are already a lot of introductory tutorials that guide you through the concepts of Nextflow and its language. In order to understand the exercises described here, it helps to have a basic understanding for which we kindly direct you to any of the following tutorials/documentation: 

- [Introductory video](https://www.youtube.com/watch?v=SYhDkUgcOXo&feature=emb_logo)  
- [Basic concepts](https://www.nextflow.io/docs/latest/basic.html)  
- [Nextflow tutorial by CRG](https://biocorecrg.github.io/ELIXIR_containers_nextflow/nextflow.html)
- [Nextflow tutorial by VIB](https://github.com/vibbits/nextflow-jnj)


**Environment setup**:  
In order to get started we need to make sure that all technical requirements are met & install Nextflow:
- Java version 8 or later
- [Nextflow](https://www.nextflow.io/docs/latest/getstarted.html)  
- [Conda](https://docs.anaconda.com/anaconda/install/)   
- [Docker](https://docs.docker.com/get-docker/)  

[Install and get started](https://www.nextflow.io/docs/latest/getstarted.html)  

## 2. Knowing where to find a pipeline and which one to use.
Once we have a fundamental understanding of the concepts of Nextflow, we can think about running our first pipeline. However, before thinking of writing our own (plausibly) complex pipeline, we can also think about importing one. Several repositories exist that store Nextflow pipelines (non-exhaustive list):  
    - Some curated nextflow pipelines are available on [awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow).  
    - Pipelines from the [nf-core community](https://nf-co.re/pipelines).  
    - Pipelines from [WorkflowHub](https://workflowhub.eu/) (this is a currently ongoing effort).  
        
````{admonition} Exercises
:class: note

2.1 How many pipelines are currently available in [nf-core](https://nf-co.re/)? How many are under development, released, and archived?

2.2 Find the pipeline doing ATAC-seq data analysis in [nf-core](https://nf-co.re/). 
- What is the current/latest version of the pipeline? 
- How many versions are available to download? 
- How many and which paramater(s) is(are) **required** to run the pipeline? 
- What is the default output directory's name? 
- What happens if you do not specify a profile (`-profile`)?

2.3 In the [nextflow-io *awesome* pipelines](https://github.com/nextflow-io/awesome-nextflow), look for the featured `BABS-aDNASeq` workflow:
- What tool is used for calling variants?
- What version of Nextflow is it advised to use?
- How do you download the `BABS-aDNASeq` pipeline locally?
````



## 3. Import a pipeline 

A curated list of available pipelines  can be found on [awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow). For the purpose of this tutorial we will use the [nextflow-io/rnaseq-nf](https://github.com/nextflow-io/rnaseq-nf) pipeline. A toy workflow for the analysis of RNAseq data.

The first thing to understand is which are the different possibilities we have to pull a pipeline publicly available at a git-based hosting code system (GitHub, GitLab or BitBucket). 

````{admonition} Exercises
:class: note

3.1 Try to pull the pipeline from your command line. 

3.2 The latest version of the pipeline is implemented using DSL2, the new syntax extension enables Nextflow to use modules. Imagine that you would like to run the last DSL1 version of the pipeline (v1.2), which command could you use to pull this specific version?

3.3 Nextflow enables to pull any specific tag, release or commit. Now try to use the same option to pull the pipeline from (1) a given branch and at a (2) specific git commit.
```` 
    
## 4. Execute a pipeline

After importing our pipeline of interest, we can run it on the command-line using the `nextflow run <pipeline-name>` command, with `<pipeline-name>` being the name of the pipeline we just imported. This is the fundamental command of running a nextflow pipeline, however will be further explored during the upcomming sessions with more details. 

````{admonition} Exercises
:class: note

4.1 Run the `rnaseq-nf` pipeline. 

```{note}  
When you use `nextflow run` without pulling the pipeline first (`nextflow pull`), the pipeline will also immediately be fetched from GitHub and run locally. 
```  

```{warning}
If an error appears to the screen similar to the one described here: `Command error: .command.sh: line 2: salmon/fastqc/multiqc: command not found`, it means that the tools are not installed. There are several ways how to fix this, e.g. install the tools locally or by using environment managers or containers (see later). 
```    

````

    
Sometimes you do not have the admin rights to install the tools used in a Nextflow pipeline. In this case it is useful to know that Nextflow supports several environment managers such as Conda, Docker and Singularity. In section 7, we will discuss how to change the defaults. 

````{admonition} Exercises
:class: note


4.2 Run the pipeline with a different environment manager, namely `Docker`. Find a parameter that you need to add when running the pipeline on the command line by using `nextflow run -h` 


4.3 With the reproducibility aspect in mind, at a certain point we want to be sure that we are running a specific version of the pipeline. Use the command that you created in the previous exercise and extend it so it runs a specific released version of the pipeline (v1.2).

4.4 (advanced) Besides Docker containers, it is also possible to run the pipeline with conda or singularity. Edit the command, so it uses the appropriate environment manager.

````




## 5. Locate and describe the output after running a pipeline.
The execution of the pipeline generates an output similar to the one defined below. We can extract a lot of useful information from this output, e.g. which version of Nextflow, which version of the pipeline, the processes that were run in the pipeline, etc. This information is always printed out, however depending on how the pipeline script is written, it is possible to include some more details, e.g. the parameters that were used (reads, transcriptome and output directory), the duration and resources usage. 

```
N E X T F L O W  ~  version 20.10.0
Launching `nextflow-io/rnaseq-nf` [high_morse] - revision: 98ffd10a76 [master]
R N A S E Q - N F   P I P E L I N E
 ===================================
 transcriptome: /path/to/.nextflow/assets/nextflow-io/rnaseq-nf/data/ggal/ggal_1_48850000_49020000.Ggal71.500bpflank.fa
 reads        : /path/to/.nextflow/assets/nextflow-io/rnaseq-nf/data/ggal/*_{1,2}.fq
 outdir       : results
executor >  local (6)
[ee/5aa84a] process > RNASEQ:INDEX (ggal_1_48850000_49020000) [100%] 1 of 1 ✔
[2b/456337] process > RNASEQ:FASTQC (FASTQC on ggal_liver)    [100%] 2 of 2 ✔
[ec/d69890] process > RNASEQ:QUANT (ggal_gut)                 [100%] 2 of 2 ✔
[3d/17a04c] process > MULTIQC                                 [100%] 1 of 1 ✔
Done! Open the following report in your browser --> results/multiqc_report.html
Completed at: 01-Jan-2021 01:23:45
Duration    : 10m 13s
CPU hours   : (a few seconds)
Succeeded   : 6
```

````{admonition} Exercises
:class: note


5.1 Have a look in the folder from where you ran the pipeline. Which directories and files have been created? 

5.2 All the output generated by the pipeline will be stored in the `work/` directory. This folder contains a bunch of subfolders that store the (intermediate) output of the pipeline. Based on the output of running the pipeline, can you find out in which folder the results of the multiqc step is being stored?  

5.3 Go to the directory that contains the outputs of a given step e.g. `RNASEQ:QUANT`.
- Find out which files are present in that folder. What does the `->` symbol mean? 
- Find for that process which command was given to the computer. 
- Advanced: how can you change the behaviour of storing the files in the output directory? (hint have a look in the documentation and search for a parameter `publishDir`)?   

````
 
 
## 6. Run a pipeline with different parameters.

**1. Pipeline parameters**:

The parameters defined in the `main.nf` [script](https://github.com/nextflow-io/rnaseq-nf/blob/master/main.nf) are parameters related to running the pipeline and can be modified/overwritten on the command-line with a double dash: e.g parameter `params.param1` in the `main.nf` script can be set as `--param1` in the command-line.

````{admonition} Exercises
:class: note

6.1 Try to modify the name of the folder where results are dumped by using a different parameter on the command-line.


6.2 What other parameters can you modify in the rnaseq-nf pipeline?
 

````

**2. Nextflow parameters**:

Nextflow-specific parameters are set in the command-line with a **single** dash and are predefined in Nextflow's language.  

````{admonition} Exercises
:class: note

6.3 Nextflow has a built-in parameter that allows us to run the pipeline in the background (hence no need of `nohup` or `screen`) and one that allows us to resume a pipeline when it failed at a given process. These are very helpful and time-saving features. Which parameters do we need to add on the command-line to request such behaviour? 
    

````

## 7. Configuration files
Lastly, the configuration files (`nextflow.config`) allow us to set technical parameters overlooking how the pipeline is being run. The standard is to write parameters related to the infrastructure (HPC clusters, cloud computing, resources, etc.) or environment managers/containers (Conda, Docker and Singularity) in so-called `profiles`. Once defined, these profiles can be chosen on the command-line and allow us to easily choose these sets of parameters based on the infrastructure we want to use for running our pipeline. 

````{admonition} Exercises
:class: note

7.1 Run with profile (standard & -with-docker) or (standard,docker) or (standard,conda)  
- `nextflow run nextflow-io/rnaseq-nf -profiles standard -with-docker`. Actually, by default the local executor will be chosen and it is hence not necessary to select the `standard` profile.   
- `nextflow run nextflow-io/rnaseq-nf -profiles standard,docker`  
- `nextflow run nextflow-io/rnaseq-nf -profiles standard,conda`


7.2 (advanced) Knowing the above, change the parameters of the `standard` profile so it takes different reads. How does the pipeline react, which reads are being used as inputs?   
- To change anything in the configuration file, the `nextflow.config` file needs to be in the same directory from where we are running the pipeline. For this, you can use the following command: `nextflow clone <pipeline-name>` to download the pipeline locally. Then, open an editor and change the `nextflow.config` file so it contains the following:
```
standard {
    process.container = 'quay.io/nextflow/rnaseq-nf:latest'
    params.reads = "$baseDir/data/ggal/ggal_liver_{1,2}.fq"
 }
```

````

