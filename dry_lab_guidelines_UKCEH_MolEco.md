:construction: Under construction !!! :construction:

These are our **dry-lab guidelines** for **data and project organization**.

**Disclaimer**: These guidelines should define the **minimal project requirements**. The use of some of the tools is **mandatory**, e.g. `git` and this `GitHub/GitLab` platform, while other tools are only listed as recommendations. You are free to adapt the suggested setup to your needs and preferences as long as the chosen tools ensure the minimal requirements described here.
Also, feel free to propose changes and corrections, and to ask questions if something is not clear.

For information on the group and (neo)huxley servers, please see [here](Dry-lab-servers).

# Basic rules

- each project should have a **repository**, and a designated **place for raw data and results** which is **backed up** (see below)
- for large projects use the **(neo)huxley servers** or our **group servers** (see [here](Dry-lab-servers#servers))
- especially on the servers, pay attention to your **storage consumption** (see [here](Dry-lab-cleanup))
- do **not** download databases/datasets and do **not** install tools in non-user folders (see [here](Dry-lab-servers#datasets-databases-and-tools))
- make sure you know what you are doing then **changing permissions** on files/folders (see below)

# Data

:exclamation: *mandatory*

- **where**
  - on `(neo)huxley`
    - finished projects: `/mnt//projects/<project>/`
    - ongoing projects:  `/work/projects/<project>/`
  - on group servers
    - *TODO*
- **how**: main folders
  - `raw/`: raw data files
    - (after we have established the raw data organization, these will be only `symlinks`)
    - remove write-permissions from raw data files/folders
  - `data/`: additional data, e.g. metadata, external data
    - remove write-permissions from relevant files/folders
  - `repo/`: cloned repository
  - `wiki/`: cloned repository wiki
  - `analysis/`: final results
  - `users/`: preliminary results, in **sub-folders** `<ulogin>/`

After a project has been **finished** make sure to
- **remove** redundant data
- **compress** files and folders if possible
- **remove write permissions** from important files and folders if possible

*Note: See also [Dry-lab cleanup](Dry-lab-cleanup).*

# Repository

:exclamation: *mandatory*

There should be (at least) **one private** GitHub/GitLab repository containing a **wiki** and **all** the code used to do the analysis. Additional repositories should be avoided, except for public repositories for publications (see below) and sub-projects which, for some reason, cannot or should not be part of the main repository.

When creating a new project:
- [GitHub/GitLab](https://github.com/)
- **Project name/slug**:
  - as short and descriptive as possible, ideally the acronym from the corresponding grant application
  - allowed characters: letters, digits, `-`, `_`
- **Project URL**: `https://github.com`, i.e. the **namespace** should be `moleco`
  - see [here](Dry-lab-git#GitHub/GitLab-create-a-new-project) how to create a new project
  - see [here](Dry-lab-git#GitHub/GitLab-transfer-a-project) how to transfer an existing project
- **Visibility Level**: **Private**, exceptions are
  - implementation of a tool for public use
  - public (sub-)repositories for publications (to store a copy of the final code version)

*Note: if the repository is public, make sure that it does not contain **any** sensitive data in its code, wiki, milestones, issues etc.*

Project content:
- **Code**
  - `README.md` (you can have multiple, i.e. per analysis sub-folder)
  - `.gitignore`: (content depends on your project and setup)
    - [a basic extensive template](https://github.com/jcchouinard/SEO-Projects/blob/master/.gitignore), [GitHub templates](https://github.com/github/gitignore)
  - one sub-folder per analysis/workflow/user
    - [template for project structure](https://snakemake.readthedocs.io/en/stable/snakefiles/deployment.html#distribution-and-reproducibility) when using `snakemake` (also useful for other set-ups)
- **Wiki**:
  - projects description
  - `md5sum` files (for relevant external data)
  - any relevant project information and notes

*Note: for more information on `git` see also [Dry-lab git](Dry-lab-git).*

## Code

:information_source: *info/recommendations*

Suggestions for tools for workflow and tools management:
- Pipelines
  - [snakemake](https://snakemake.github.io/) (recommended)
  - [targets](https://books.ropensci.org/targets/) for `R`-pure pipelines
  - [nextflow](https://www.nextflow.io/)
- Software
  - Conda (can be used together w/ `snakemake`) (recommended)
    - [Conda](https://docs.conda.io/projects/conda/en/latest/index.html)
    - [Miniconda](https://docs.conda.io/en/latest/miniconda.html)
    - [Anaconda](https://anaconda.org/)
  - EasyBuild
    - TODO: link to documentation
    - TODO: (neo)huxley tutorial(s)
- Container
  - [docker](https://www.docker.com/)
  - [singularity](https://singularity.lbl.gov/)

If no tool management system is used you should provide a `README` describing
- versions of all relevant tools (incl. dependencies)
- installation instructions, incl. download links

## Documentation

:exclamation: *mandatory*

Using the repositories' **wiki** to save relevant notes and information about the projects and the analysis is **compulsory**.
Large relevant documents (e.g. metadata and presentations) can be saved together with the data on the server(s) in the folder `data/`.
Create `README` files in the code repository to describe how to re-run your workflow or analysis.

:information_source: *info/recommendations*

Using GitHub/GitLab's issue system, is a great way to document project's progress.
Issues can be used to keep track of things to be done.

# Working directory

:information_source: *info/recommendations*

Depending on how much data you have and whether you are collaborating with someone, write your results to

- your `HOME` directory: `~/<project>/` (`/mnt/(neo)huxleygpfs/users/<ulogin>`) (for small projects)
- your folder on `scratch`: `/scratch/users/<ulogin>/<project>` (recommended)

# File permissions

:information_source: *info/recommendations*

If you do not know about Linux file permissions, please familiarize yourself with this topic, e.g. [here](https://www.linux.com/training-tutorials/understanding-linux-file-permissions/).

- do **NOT** use `chmod 777 <files/folders>` or `chmod o+rwx <files/folder>`
  - most of the time you will not need to give users outside of your group all permissions to your files/folders
- use the flag `-R` to change permissions of a folder **recursively**
- a **folder** is only **readable** if the bits `r` **and** `x` are set
- do **NOT** make files executable (set bit `x`) if they are not intended for execution
  - e.g. there is no reason to make a FASTA file executable
- remove **write permissions** from **important files** to avoid overwriting them
  - **IMPORTANT**: deleting them with `rm -f` will still work
- remove **write permissions** from **important folders** to avoid deleting their files by accident (even when using `rm -f`)
  - **IMPORTANT**: modifying existing files will still work

Useful references:
- [Linux: managing file permissions](https://www.linux.com/training-tutorials/how-manage-file-and-folder-permissions-linux/)
- [Linux: chmod calculator](https://chmod-calculator.com/)
