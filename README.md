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

## About DVC-CC
This branch was automated created with the tool DVC-CC. This tool connects DVC (https://dvc.org/) to CC (www.curious-containers.cc) to run your defined stages with DVC in a docker on your cloud system with CC. [More information about DVC-CC](https://github.com/deep-projects/dvc-cc)

## DVC-Status


<details><summary>Before Execution</summary>
<p>

```
WARNING: Output 'tensorboard'(Stage: 'dvc/train.dvc') is missing version info. Cache for it will not be collected. Use dvc repro to get your pipeline up to date.
WARNING: Output 'tf_model.h5'(Stage: 'dvc/train.dvc') is missing version info. Cache for it will not be collected. Use dvc repro to get your pipeline up to date.
WARNING: Output 'outputs/all-history.json'(Stage: 'dvc/train.dvc') is missing version info. Cache for it will not be collected. Use dvc repro to get your pipeline up to date.
WARNING: Output 'outputs/history-summary.json'(Stage: 'dvc/train.dvc') is missing version info. Cache for it will not be collected. Use dvc repro to get your pipeline up to date.
Data and pipelines are up to date.

```

</p>
</details>




<details><summary>After Execution</summary>
<p>

```
	new:                tensorboard
	new:                tensorboard/train/events.out.tfevents.1573287395.3eabc6f5dfee.219.543.v2
	new:                tensorboard/train/events.out.tfevents.1573287397.3eabc6f5dfee.profile-empty
	new:                tensorboard/train/plugins/profile/2019-11-09_08-16-37/local.trace
	new:                tensorboard/validation/events.out.tfevents.1573287417.3eabc6f5dfee.219.43299.v2
	new:                tf_model.h5
	new:                outputs/all-history.json
	new:                outputs/history-summary.json

```

</p>
</details>



## How to rerun this experiment:
The following sections describe how you can rerun the dvc stages yourself.


<span style="color:red">Warning: During execution a folder was included via sshfs.</span>


### Pure command line (run the experiment local)
```
sh source/download_pcam.sh
python source/train.py --learning-rate 0.04936777408792682 --batch-size 128 --num-of-epochs 200 --activation-function relu --kernel-width 4 --average-kernels 116 --num-of-conv-layers 4 --kernel-increasing-factor 0.9369641460763412 --maxpool-after-n-layer 1 --dropout-factor-after-conv 0.1417187279371753 --dropout-factor-after-maxp 0.01

```
### Using DVC (run the experiment local)
```
dvc repro -P
```
### Using CC (run the experiment on a server)
```
faice exec cc_execution_file.red.yml
```
## Executed System
The scipt ran on the following system:


<details><summary>GPU(s)</summary>
<p>

```
                          name    memory.total [MiB]
====================================================
           GeForce GTX 1080 Ti             11178 MiB

```

</p>
</details>




<details><summary>Other Hardware</summary>
<p>

```
H/W path              Device  Class       Description
=====================================================
/0/0                          memory      62GiB System memory
/0/1                          processor   AMD Ryzen 7 1800X Eight-Core Processor

```

</p>
</details>




<details><summary>Software</summary>
<p>

```
Package              Version      
-------------------- -------------
absl-py              0.8.0        
appdirs              1.4.3        
asciimatics          1.11.0       
asn1crypto           0.24.0       
astor                0.8.0        
atpublic             1.0          
attrs                19.2.0       
backcall             0.1.0        
bcrypt               3.1.7        
bleach               3.1.0        
certifi              2019.9.11    
cffi                 1.12.3       
chardet              3.0.4        
colorama             0.4.1        
configobj            5.0.6        
configparser         4.0.2        
contextlib2          0.5.5        
cryptography         2.7          
cycler               0.10.0       
decorator            4.4.0        
defusedxml           0.6.0        
distro               1.4.0        
dvc                  0.60.1+ee976a
dvc-cc-agent         0.8.8        
dvc-cc-connector     0.8.1        
entrypoints          0.3          
flufl.lock           3.2          
funcy                1.13         
future               0.17.1       
gast                 0.2.2        
gitdb2               2.0.6        
GitPython            3.0.2        
google-pasta         0.1.7        
grandalf             0.6          
grpcio               1.24.0       
h5py                 2.10.0       
humanize             0.5.1        
idna                 2.6          
inflect              2.1.0        
ipykernel            5.1.2        
ipython              7.8.0        
ipython-genutils     0.2.0        
ipywidgets           7.5.1        
jedi                 0.15.1       
Jinja2               2.10.1       
joblib               0.14.0       
jsonpath-ng          1.4.3        
jsonschema           3.0.2        
jupyter              1.0.0        
jupyter-client       5.3.3        
jupyter-console      6.0.0        
jupyter-core         4.5.0        
Keras-Applications   1.0.8        
Keras-Preprocessing  1.1.0        
keyring              10.6.0       
keyrings.alt         3.0          
kiwisolver           1.1.0        
Markdown             3.1.1        
MarkupSafe           1.1.1        
matplotlib           3.1.1        
mistune              0.8.4        
mock                 3.0.5        
nanotime             0.5.2        
nbconvert            5.6.0        
nbformat             4.4.0        
networkx             2.3          
notebook             6.0.1        
numpy                1.17.2       
opt-einsum           3.1.0        
packaging            19.2         
pandas               0.25.1       
pandocfilters        1.4.2        
paramiko             2.6.0        
parso                0.5.1        
pathspec             0.5.9        
pexpect              4.7.0        
pickleshare          0.7.5        
Pillow               6.2.0        
pip                  19.2.3       
ply                  3.11         
prometheus-client    0.7.1        
prompt-toolkit       2.0.9        
protobuf             3.9.2        
ptyprocess           0.6.0        
pyasn1               0.4.7        
pycparser            2.19         
pycrypto             2.6.1        
pyfiglet             0.8.post1    
Pygments             2.4.2        
pygobject            3.26.1       
pyjson               1.3.0        
PyNaCl               1.3.0        
pyparsing            2.4.2        
pyrsistent           0.15.4       
python-dateutil      2.8.0        
pytz                 2019.2       
pyxdg                0.25         
PyYAML               5.1.2        
pyzmq                18.1.0       
qtconsole            4.5.5        
red-connector-ssh    1.0          
requests             2.22.0       
ruamel.yaml          0.16.5       
ruamel.yaml.clib     0.2.0        
schema               0.7.1        
scikit-learn         0.21.3       
scipy                1.3.1        
scp                  0.13.2       
seaborn              0.9.0        
SecretStorage        2.3.1        
Send2Trash           1.5.0        
setuptools           41.2.0       
shortuuid            0.5.0        
six                  1.11.0       
sklearn              0.0          
smmap2               2.0.5        
tensorboard          2.0.0        
tensorflow-estimator 2.0.0        
tensorflow-gpu       2.0.0        
termcolor            1.1.0        
terminado            0.8.2        
testpath             0.4.2        
torch                1.2.0        
torchvision          0.4.0        
tornado              6.0.3        
tqdm                 4.36.1       
traitlets            4.3.2        
treelib              1.5.5        
urllib3              1.25.6       
wcwidth              0.1.7        
webencodings         0.5.1        
Werkzeug             0.16.0       
wheel                0.30.0       
widgetsnbextension   3.5.1        
wrapt                1.11.2       

```

</p>
</details>


