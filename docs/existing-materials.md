# Overview existing materials
This page contains an overview of current materials on the topic of Containers (Docker & Singularity) and Workflow pipelines (Nextflow & Snakemake) with a focus on Life Sciences research. Any other suggestions, please reach out! 

## Containers

- https://biocorecrg.github.io/ELIXIR_containers_nextflow/

Notes: ELIXIR course "Containers and Workflow Pipelines for reproducible and automated data analysis": Two full day hands-on course (run online) with materials created by CRG Bioinformatics Core. The course has been organized and supported by the VIB Bioinformatics Core. The course materials are available on GitHub. Technical setup: Ubuntu on GCE, everyone had access to the same machine (duplicate for each participant) approachable with VNC. 

- https://github.com/vibbits/nextflow-jnj

Notes: [theory materials](https://elearning.bits.vib.be/courses/introduction-to-docker/) on introductiory level for Docker & Singularity in ‘e-learning’ format, exercises in GitHub repository linked to RNA-seq. Accompanied with exercises that focus on using containers rather than how to build them. These materials should hence familiarize students on how to use these technologies. 

- https://sib-swiss.github.io/containers-introduction-training/ 

Notes: inspired by https://carpentries-incubator.github.io/docker-introduction/ with extension of Singularity material. Cherry picked since combination of docker and singularity. Technical setup: NGS courses set up with Amazon cloud server, with login ssh (bash code for setup here: https://github.com/geertvangeest/AWS), all tools provided with conda and accompanying yml file ([example](https://sib-swiss.github.io/NGS-variants-training/day1/server_login/))

- https://ome.github.io/training-docker/
- https://carpentries-incubator.github.io/docker-introduction/

- https://carpentries-incubator.github.io/singularity-introduction
- https://nbis-reproducible-research.readthedocs.io/en/latest/

Notes: Covers a broad range of topics: conda, snakemake, git, Jupyter, R markdown, singularity. Planned to be hosted biannually. 

- https://github.com/orchid00/The_Carpentries_info/blob/master/carpentries_style_shared_lessons.md#docker--singularity---containers


## Workflow pipelines
### Nextflow
- https://biocorecrg.github.io/ELIXIR_containers_nextflow/

Notes: ELIXIR course "Containers and Workflow Pipelines for reproducible and automated data analysis": Two full day hands-on course (run online) with materials created by CRG Bioinformatics Core. The course has been organized and supported by the VIB Bioinformatics Core. The course materials are available on GitHub. Technical setup: Ubuntu on GCE, everyone had access to the same machine (duplicate for each participant) approachable with VNC. Alternative: https://aws.amazon.com/cloud9/ allows you to connect to cloud instance via browser, with a terminal and text editor in the browser. Introduction to nextflow, material in DSL2 (workflows, modules), examples with RNAseq sequence, mapping, QC. 

- https://github.com/vibbits/nextflow-jnj

Notes: ELIXIR BE - VIB BITS Nextflow workshop: workshop materials (mainly) in DSL2 after brief introduction into DSL1 aiming to get familiar with the Nextflow syntax by explaining basic concepts and building a simple RNAseq pipeline. Highlights also reproducibility aspects with adding containers (docker & singularity). Slides available [here](https://github.com/vibbits/nextflow-jnj/blob/master/presentation/slidedeck.pdf). 

- https://seqera.io/training/
- https://www.nextflow.io/blog/2020/learning-nextflow-in-2020.html

Notes: links to a variety of tutorials and workshops by and for Nextflow. Courses for different entry-levels. 

- https://nf-co.re/usage/nf_core_tutorial

Notes: Course getting started with nf-core: nf-core intro, how to run pipelines, short intro for git (CI with github actions), create nextflow profile, create a nf core pipeline, touch on conda environment, final updates are being done atm regarding DSL2. Level of participants: advanced users (for developing pipelines), but beginners also for users who want to run pipelines 

- https://biocorecrg.github.io/CRG_Containers_Nextflow/

Notes: Similar content as https://biocorecrg.github.io/ELIXIR_containers_nextflow/. 

- https://bovreg.github.io/nf-workshop20/ 

Notes: Extensive Nextflow training including a containers section. Based on sequera course, 4 days, online, section for Groovy. 

- https://github.com/nextflow-io/awesome-nextflow#tutorials

Notes: Awesome Nextflow provides an overview of curated pipelines, tutorials, modules collectoins, presentations and videos. 
  
 
### Snakemake
- https://carpentries-incubator.github.io/workflows-snakemake
- https://snakemake.readthedocs.io/en/stable/tutorial/tutorial.html
- https://edwards.sdsu.edu/research/snakemake-tutorial/
- https://ulhpc-tutorials.readthedocs.io/en/latest/bio/snakemake/
- https://nbis-reproducible-research.readthedocs.io/en/latest/

Notes: Covers a broad range of topics: conda, snakemake, git, Jupyter, R markdown, singularity. Planned to be hosted biannually. 

- https://www.hpc-carpentry.org/

Notes: Analysis pipelines and parallel computing with Python (), Snakemake is embedded in this course. 

- https://escience-academy.github.io/lesson-parallel-python/

Notes: Parallel Programming in Python (escience-academy.github.io), Snakemake is embedded in this course and a use-case for parallisations

- https://coderefinery.github.io/reproducible-research/04-workflow-management/

Notes: stepping up the game of reproducibility. This short tutorial contains different ways of solving the same exercise, each time a bit more automated and reproducible, until in the last step a Snakemake pipeline is created and run.  