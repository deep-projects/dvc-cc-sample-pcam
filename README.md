This is a sample project that demonstrates the usage of DVC-CC. To find out more about DVC-CC, take a look at section three of this README.

# 1. How this repository was build

1. create a new repository
2. call "dvc-cc init"
3. add source code for downloading the pcam dataset
4. using sshfs to connect to the data storage server
5. create a dvc file for downloading the file and run it
6. create the source code
7. create a .hyperopt file
8. commit and push to git
9. run experiments with "dvc-cc run"

Here are two youtube videos that show all the steps that were done to create this repository.
- https://www.youtube.com/watch?v=HYFU7M8XSN0&feature=youtu.be
- https://www.youtube.com/watch?v=oV95aduSVtU&feature=youtu.be

# 2. Use this repository

What you can do with this git repository depends on your rights.

1. If you have read access to this git repository, you can switch to a resulting branch, a git branch that begins with 'rcc_'. You can do this by calling 'git checkout rcc_...'. In the README.md you find all pieces of information about the docker in which the experiment ran, and you find the ways to reproduce the experiment locally.
2. If you have also read access to the dvc storage server, you can get all output files, including large files.
    - For this, you can switch to a resulting branch and call 'dvc pull'. You will see now all the output files for this branch.
    - You can also take a look at multiple experiments/branches. To do this, you need first to sync all git branches with "dvc-cc git sync" and then pull, for example, the tensorboard folders of the 5th to 7th experiment with the command: 'dvc-cc output-to-tmp tensorboard -p 5:7'.
3. If you have rights to the agency, you can check the status of the last experiments with "dvc-cc status".
4. If you have all read and write rights, you can run new jobs by calling "dvc-cc run expname".

# 3. About DVC-CC

In this git repository, the software tool DVC-CC is used. This software tool makes it possible to defining experiment pipelines and runs these pipelines in a cluster. The goal of DVC-CC is to make the defined pipelines scalable, by running multiple experiments parallel in a cluster, and reproducibility, by calculating checksums for input and output files or directories.

To handle the scalability, DVC-CC uses the software Curious Containers (CC). CC allows it to start experiments in a cluster by only defining one RED file. DVC-CC creates GIT input branches that begin with "cc_". In this input branches, all hyperparameters are set and a RED file is generated. In the cluster, a DVC-CC docker image is started that downloads the source code from the GIT repository of the input branch, runs the pipeline and pushes the result to a new branch that begins with rcc_. [Here](https://www.curious-containers.cc) you can read more about Curious Containers.

To define reproducible pipelines and handle large files, DVC-CC use the Software Data Version Control (DVC). DVC outsource large output files from git to a storage server and save large files with checksums. Take a look at [this site](https://dvc.org/) to read more about DVC.

You can install the used DVC and DVC-CC version with:

```
pip install --upgrade dvc=0.66.10
pip install --upgrade dvc-cc=0.8.59
```

If you want to find out more about DVC-CC you can visit [this GitHub site](https://github.com/deep-projects/dvc-cc/tree/master/dvc-cc).

