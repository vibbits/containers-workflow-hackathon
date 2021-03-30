# Nextflow materials
Contributors Persona 1: Sarah Bonnin, Toni Hermoso Pulido, Renuka Kudva, Tuur Muyldermans  
Contributors Persona 2: Luca Cozzuto, Jose Espinosa-Carrasco, Maxime Garcia 

## Nextflow users (persona 1)
Nextflow users (more introductory - concepts why - exercises explaining fundamentals)

### Learner's profiles
- Who are they?
    - Already have some background with bioinformatics data analysis → “Applied” bioinformaticians?
    - Linux users → they know how to use CLI 

- What problem are they having?
    - Big data, or multiple experiments with similar data and/or many data files → automate processes 

- How will the tutorial/workshop help them?
    - Understand conceptually, Understand how to run, debugging - know what which 
    - errors might mean what, resuming/retry, workdir, if process fails → where to find fails (.command./* ), .nextflow.pid
    - Reproduce failing process from workdir (maybe coupled to run from associated container)
    
    
### Learner's objectives

- Prerequisites for the course/tutorial
    - They have some (basic) experience in CLI/Linux, so they are able to run a pipeline and understand what’s happening or tune the parameters etc. 
    - linux users, Dataflow, so conceptually, git / GitHub  

<!--
Basic knowledge of Linux/command-line. Familiar enough to navigate through the folders, inspect and change files (with nano or any other text-editor of preference), more than just running the literal commands given in the ‘course’.
-->


- Define exercises with learning outcomes (measurable)*
    - Describe terminology/different concepts so you can explain to a developer what might need to be changed. 
    - To be able to find and run different existing pipelines. 
    - Do small trouble-shootings yourself (unrelated to the programming of the pipeline - at the level of config file). 
    - Navigate the workdir and find specific output(files). 
    - raise issues or reach out to the community

*Goals: “After following one of these tutorials, learners will be able to …” 



### Training materials

Outline: 
- Introduction nextflow and language 
    - Describe nextflow conceptually and the language. 
    - Describe the concepts of channels, operators, processes, modules 
- Knowing where to find a pipeline (github, nf-core, ...) and which one to use. 
- Import a pipeline (download/clone locally or from github - but also possible to pull (nextflow pull)) https://github.com/nextflow-io/awesome-nextflow 
    - Exercise: `nextflow run <pipeline>`  (toy pipelines = tiny pipelines) + fast, easy, simple. When more familiar → then go to a nf-core pipeline.
    - Exercise: nextflow-pull a specific pipeline (they need to find themselves). Extra: define release (or tag/release/commit)
    - Exercise: git clone so they have a pipeline where they can work on / alternatively: create config file that will overwrite the config file.

- Explain config files and being able to do minor modifications (eg. change version of docker container, parameters like computation power)
    - Config files: there might be parameters related to running things in the cloud/HPC which you are not allowed to change, but there might be also one related to the pipeline (so more regarding the bioinformatics tools)
    - Exercise inspect the config file and change a parameter (an easy one) and it should be clear that when you have changed it it gives a different output
    - profiles: Exercise with different profiles (if possible)
- Execute a pipeline
    - Exercise nextflow run `<pipeline>`  (toy pipelines = tiny pipelines) + fast, easy, simple. When more familiar → then go to a nf-core pipeline. 
- Locate and describe the output after running a pipeline → workdir with different files (.command.*). 
    - Exercise when running the pipeline it created an output. Find where the output was created. 
    - Exercise: find for that process which command was given to the computer (.command.sh)
- Identify the different parameters : nextflow-specific versus pipeline-specific (- vs --) 
    - Running in the background
    - Resume pipeline 
        - Exercise delete a workdirectory and see that the pipeline resumes from somewhere else (in the beginning) people should be aware of the fact that it becomes very big. Some pipelines allow you to cp or mv the results inside the directory that you want (there is a parameter/flag for it so not necessary to change it inside the pipeline script). 
        - Showcase the caching - run with a different parameter (file or the file has moved). When the file has moved → different timestamp → different cache. 
- Create reports
    - Exercise where they create a visual report: (-with-dag)
    - Exercise where they create a html report (-with-report)
    - Running with Tower. 

- Analyze the error/failure of a pipeline - correct it appropriately (if technical is not relevant) 
    - lack of memory and resources, file not found, docker not provided, error related to the tool (find it in the error message of the pipeline or in the workdir : .command.out/err) 
    - One hyphen or two hyphen, wrong dash, file missing, missing parameter.
    - Exercise: find for that process which command was given to the computer (.command.sh) 

Extra:
- File issue on GitHub (if relevant) or contact community 
- understand how databases are used within pipeline 
- containers/singularity?




## Nextflow pipeline developers (persona 2)

### Learner's profiles

- Who are they?
    - bioinformaticians that want to develop using nextflow (both beginners and more advanced)
- What problem are they having?
    - parallelizing, reproducibility, portability etc.
    - porting pipelines to NF
    - porting DSL1 to DSL2
- How will the tutorial/workshop help them?
    - learning basics and pointers with more resources / community etc 
    - they will know a list of useful tools / resources for programming / editing
    - debugging


### Learner's objectives

- Prerequisites for the course/tutorial
    - linux users, bash, CLI, know a programming language, git / GitHub is strongly recommended
    - containers

- Define exercises with learning outcomes (measurable)*
    - Channel, Process and Workflow (To learn Nextflow DSL2)
    - Switching to DSL2 (For users already knowing Nextflow)
    - Assembling (sub)workflows
    - Configuration (To help with controlling the resource, parameters)
        - Change docker/conda/singularity - know what they can change
    - Debug (With some examples. To help users understanding the logic and the mindset)

*Goals: “After following one of these tutorials, learners will be able to …”

### Training materials
Outline:
- Recognize that reproducibility is an advantage
    - (-> using a workflow manager makes a pipeline reproducible and save time)
    - (-> using containers)
- Remember Reproducibility
    - (Why we use workflow managers, NO MORE BASH SCRIPTS)
- Understand dataflow programming model
- Use configuration files (or profile)
- Analyze what is causing an issue/bug, and where it’s coming from
- Design their own pipeline




## Contribution notes
This Markdown-file can be collaboratively and simultaneously edited from [this link](https://hackmd.io/@tmuylder/S1B8dzFWO/edit).

Please push to the branch `nextflow` in order not to make conflicting versions. This is automatically done when you push the Hackmd-file to GitHub (click on Settings... right top --> Versions and GitHub Sync --> Push). However, might only be done by @tmuylder. 

