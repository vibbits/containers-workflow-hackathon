# Workflow pipelines

The importance of running reproducible and automated data analysis and Nextflow is gaining traction by a wide community of Life Sciences researchers and bioinformaticians to do this. Current tutorials often focus on writing your own basic pipelines, however it is not always necessary to reinvent the wheel. This tutorial and set of exercises will guide you through your first steps on how to use pipelines that are available on the internet. 

Besides Nextflow, we would also like to stress the importance of other workflow languages like [Snakemake](https://snakemake.readthedocs.io/en/stable/) and [Common Workflow Language (CWL)](https://www.commonwl.org/). A list of tutorials and workshop materials on the former is available in the [existing materials](https://containers-workflows.readthedocs.io/en/latest/existing-materials.html) page, for the latter we refer to the current efforts of the training materials being developed in the [Carpentries](https://carpentries.org/) style by the CWL community to teach workflow thinking to novices.

## Content


```{toctree}

exercises
solutions


```


## Learner's profiles

- Who are they?
    - Already have some background with bioinformatics data analysis
    - Linux users → they know how to use CLI
    - Familiarity with git / GitHub advantageous but not strictly required. They can take - for example - the dedicated [Software Carpentry tutorial.](http://swcarpentry.github.io/git-novice/)
     
- What problem are they having?
    - Big data, or multiple experiments with similar data and/or many data files → automate processes
    - Want to make their analysis reproducible

- How will the tutorial/workshop help them?
    - Understand conceptually, Understand how to run, debugging - know what which
    - errors might mean what, resuming/retry, workdir, if process fails → where to find fails (.command./* ), .nextflow.pid
    - Reproduce failing process from workdir (maybe coupled to run from associated container)
  
## Learner's objectives

- Prerequisites for the course/tutorial
    - Have an understanding of bioinformatics data analysis 
    - Experience in CLI/Linux, feeling comfortable moving around in the Terminal


- Define exercises with learning outcomes (measurable)*
    - Describe terminology/different concepts so you can explain to a developer what might need to be changed. 
    - To be able to find and run different existing pipelines.
    - Do small trouble-shootings yourself (unrelated to the programming of the pipeline).
    - Navigate the `workdir` and find specific output(files).

*Goals: “After following one of these tutorials, learners will be able to …” 



