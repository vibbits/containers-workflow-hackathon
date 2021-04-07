
## Learning objectives:
1. Introduction nextflow and language (theoretical)
2. Knowing where to find a pipeline and which one to use.
3. Import a pipeline.
4. Execute a pipeline.
5. Locate and describe the output after running a pipeline.
6. Run a pipeline with different parameters.
7. Explain config files and being able to do minor modifications.


Example pipeline: https://github.com/nextflow-io/rnaseq-nf
Tutorial based on this pipeline (focus on how to edit & construct the pipeline): https://github.com/cbcrg/nf-phdcourse20


## 1. Introduction nextflow and language (theoretical)

[Introductory video](https://www.youtube.com/watch?v=SYhDkUgcOXo&feature=emb_logo)[Basic concepts](https://www.nextflow.io/docs/latest/basic.html)
[Install and get started](https://www.nextflow.io/docs/latest/getstarted.html)

## 2. Knowing where to find a pipeline and which one to use.

Several repositories exist that store nextflow pipelines (non-exhaustive list):
        - Some curated nextflow pipelines are available on [awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow).
        - Pipelines from the [nf-core community](https://nf-co.re/pipelines).
        -  Pipelines that use the [BioContainers tools](https://github.com/BioContainers/workflows). *Obsolete?*
        
**Exercise 2**: 
* 2.1 Go to [nf-core](https://nf-co.re/):
    * How many pipelines are currently available in nf-core?
!!! solution
As of 6/04/2021:
50 pipelines
    * How many are under development, released, and archived?
!!! solution
As of 6/04/2021:
Under development: 18
Released: 28
Archived: 4


* 2.2 Find the pipeline doing ATAC-seq data analysis in [nf-core](https://nf-co.re/). 
!!! solution
https://nf-co.re/atacseq
    * What is the current/latest version of the pipeline? 
!!! solution
1.2.1 (as of 6/04/2021)
    * How many versions are available to download?
!!! solution
5 versions (as of 6/04/2021): current (1.2.1), 1.2.0, 1.1.0, 1.0.0, dev.
    * Go to the **Parameter docs** tab: 
        * How many and which paramater(s) is(are) **required** to run the pipeline?
!!! solution
Only 1 required parameter: **--input** (Path to comma-separated file containing information about the samples in the experiment)
        * What is the default output directory's name?
!!! solution
**./results** (parameter --outdir)
    * Go to the **Usage docs** tab: 
        * What happens if you do not specify a profile (**-profile**)?
!!! solution
[*If -profile is not specified, the pipeline will run locally and expect all software to be installed and available on the PATH.*](https://nf-co.re/atacseq/1.2.1/usage#main-arguments)

* 2.3 In the [nextflow-io *awesome* pipelines](https://github.com/nextflow-io/awesome-nextflow), look for the featured **BABS-aDNASeq** workflow:
!!! solution
https://github.com/crickbabs/BABS-aDNASeq
    * What tool is used for calling variants?
!!! solution
samtools mpileup
    * What version of Nextflow is it advised to use?
!!! solution
version 0.30.2
    * How do you download the **BABS-aDNASeq** pipeline locally?
!!! solution
git clone https://github.com/crickbabs/BABS-aDNASeq


## 3. Import a pipeline 

A curated list of available pipelines  can be found on [awesome-nextflow](https://github.com/nextflow-io/awesome-nextflow).

For the purpose of this tutorial we will use the [nextflow-io/rnaseq-nf](https://github.com/nextflow-io/rnaseq-nf) pipeline. A toy workflow for the analysis of rnaseq data.

The first think to understand is which are the different possibilities we have to pull a pipeline publicly available at a git-based hosting code system (GitHub, GitLab or BitBucket). 

* **Exercise 3.1** Try to pull the pipeline from your command line:
    
    ---
    **Solution**
    
    `nextflow pull nextflow-io/rnaseq-nf`
    
    ---
    
* **Exercise 3.2** The latest version of the pipeline is implemented using DSL2, the new syntax extension that enables Nextflow the use of modules. Imagine that you would like to run the last DSL1 version of the pipeline (v1.2), which command could you use to pull this specific version?
    
    ---
    **Solution**
    
    `nextflow pull nextflow-io/rnaseq-nf -r v1.2`
    
    ---

* **Exercise 3.3** Nextflow enables to pull any specific tag,release or commit. Now try to use the same option to pull the pipeline from (1) a given branch and at a (2) specific git commit.

    ---
    **Solution**
    
    `nextflow pull nextflow-io/rnaseq-nf -r master`
    
    `nextflow run nextflow-io/rnaseq-nf -r 98ffd10a76`

    ---



    
 ## 4. Execute a pipeline

After importing our pipeline of interest, we can run it on the command-line using the `nextflow run <pipeline-name>` command, with `<pipeline-name>` being the name of the pipeline we just imported. This is the fundamental command of running a nextflow pipeline, however will be further explored during the upcomming sessions with more details. 
* **Exercise 4.1**: run the `rnaseq-nf` pipeline

    ---
    **Solution**
    `nextflow run nextflow-io/rnaseq-nf`
    
    ---
    
    ---
    **Note**
    When you use `nextflow run` without pulling the pipeline first (`nextflow pull`), the pipeline will also immediately be fetched from GitHub and run locally. 
    
    ---    

    ---
    **Warning**
    If an error appears to the screen similar to the one described here: `Command error: .command.sh: line 2: salmon/fastqc/multiqc: command not found`, it means that the tools are not installed. There are several ways how to fix this, e.g. install the tools locally. Or by using 
    
    ---  
    
Sometimes you do not have the admin rights to install the tools used in a Nextflow pipeline. In this case it is useful to know that Nextflow supports several environment managers such as Conda, Docker and Singularity. In chapter 7, we will discuss how to change the defaults. 

- **Exercise 4.2**: Run the pipeline with a different environment manager, namely `Docker`. Find a parameter that you need to add when running the pipeline on the command line by using `nextflow run -h` 
 
    ---
    **Solution** 
    Docker `nextflow run nextflow-io/rnaseq-nf -with-docker`
    
    ---
- **Exercise 4.3**: With the reproducibility aspect in mind, at a certain point we want to be sure that we are running a specific version of the pipeline. Use the command that you created in the previous exercise and extend it so it runs a specific released version of the pipeline (v1.2).
    
    ---
    **Solution** 
    `nextflow run nextflow-io/rnaseq-nf -with-docker -r v1.2`

    ---
    
- **Advanced exercise 4.3**: Besides Docker containers, it is also possible to run the pipeline with conda or singularity. Edit the command, so it uses the appropriate environment manager. 
    
    ---
    **Solution** 
    Conda: the state-of-the-art way of running with conda is by using the `-with-conda` parameter. However, if the [conda environment file](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-file-manually) (here `conda.yml`) is not present in the directory where you are currently running the pipeline from, it will give an error. Therefore, the solution would be to include the path to the conda.yml file: `nextflow run nextflow-io/rnaseq-nf -with-conda path/to/conda.yml`.
    
    ---
    
    !!! solution
    Singularity: (if Singularity installed): `nextflow run nextflow-io/rnaseq-nf -with-singularity`

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

- **Exercise 5.1**: Have a look in the local folder (from where you ran the pipeline). Which directories and files have been created? 
    
    ---
    
    **Solution** 
    `.nextflow.log`, `results/` and `work/`
    
    ---

- **Exercise 5.2**: All the output generated by the pipeline will be stored in the `work/` directory. This folder contains a bunch of subfolders that store the (intermediate) output of the pipeline. Based on the output of running the pipeline, can you find out in which folder the results of the multiqc step is being stored?  

    ---
    
    **Solution** 
    
    Solution: `./work/3d/17a04c`... the actual folder name is much longer, but the short version is given here. These names are automatically generated based on a hash.  

    ---

- **Exercise 5.3**: Go to the directory that contains the outputs of a given step e.g. `RNASEQ:QUANT`.
    - Find out which files are present in that folder. What does the `->` symbol mean? 
    - Find for that process which command was given to the computer 
    - Advanced: how can you change the behaviour of storing the files in the output directory? (hint have a look in the )  
 
Solution: 
- .command.* (e.g. log that contains the output of running the tool, sh that contains the command being run on the command-line, ...), the input files are being linked from another folder (ref: `->`) and the output files are present in the folder `ggal_gut/`. 
- .command.sh
- Advanced: each module defines the process that is actually being run. 
 
 
## 6. Run a pipeline with different parameters.

* 6.1 Pipeline parameters
The parameters defined in the `main.nf` [script](https://github.com/nextflow-io/rnaseq-nf/blob/98ffd10a76278409066c983fd4ab7f6b035a2291/main.nf#L34-L37) can be modifed be setting them in the command-line with a double dash: e.g parameter **params.param1** in the main.nf file can be set as **--param1** in the command line.

6.1.1 Try to modify the name of the folder where results are dumped.

---
    
**Solution** 

    `nextflow run nextflow-io/rnaseq-nf --outdir "myAwesomeResults" -with-docker`
    
---
 
 6.1.2 What other parameters can you modify in the rnaseq-nf pipeline?
 
---
**Solution** 

    The **reads**, **transcriptome**, **outdir** and **multiqc** parameters.
---
    

* 6.2 Nextflow parameters
Nextflow-specific parameters are set in the command-line with a **single** dash.
    * Change the **--reads** parameter to **"s3://rnaseq-nf/data/ggal/lung_{1,2}.fq"** and re-run the rnaseq-nf pipeline with the **-resume** parameter. What processe(s) are(were) *cached* ?
    
---
**Solution** 

    `nextflow run nextflow-io/rnaseq-nf --reads "s3://rnaseq-nf/data/ggal/lung_{1,2}.fq" -with-docker -resume`
    # ERROR: No files match pattern `lung_*{1,2}.fq` at path: /rnaseq-nf/data/ggal/ !!! Something might need to be set for the AWS access?

---
    
## 7. Explain config files and being able to do minor modifications.

