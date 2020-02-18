
# How to create Virtual Environment with Conda
This document describe how to use conda to create virtual environment

## Getting Started
You need to install Anaconda before following this document: https://www.anaconda.com/distribution/

### Prerequisites
On your system, you need to have the following application installed:
- Anaconda
- Python: https://www.python.org/downloads/
- Once Anaconda is installed, please open **Anaconda Prompt** The commands below need to be executed inside the Anaconda Prompt

### Virtual Environment Creation
```
conda create -n conda-env python=3.7   # or uses --name
conda activate conda-env               # activate environment
conda deactivate                       # deactivate environment
```
After the conda Virtual Environment was created, it is located under `%USERPROFILE%\Anaconda3\envs` (on Windows) 
Screnshot below shows the Virtual Environment created after the above command

![conda1](https://user-images.githubusercontent.com/57285863/74614320-33993e00-5117-11ea-910f-2f9e8a70aba1.png)

![conda2](https://user-images.githubusercontent.com/57285863/74614324-3f850000-5117-11ea-9ebf-a979599ff31c.png)

**Tips**: Similar to `venv`, the virtual environment can be created directly inside the project folder by using this command:
```
conda create -p /project_path/conda-env   # or use --prefix
```
**Note**: conda can no longer activate the virtual environment with the `--name` flag. Instead the environment has to be activated with the full project path ` /project_path/conda-env`
To fix the virtual environment display, the `env_prompt` setting in the `.condarc` file need to be modified with the following command:
```
conda config --set env_prompt '({name})'
```
### Packages Installation using conda
#### Packages Installations from the Anaconda Repository
Before proceeding, the target environment need to be activated first with command:
```
conda activate conda-env
```
```
conda install pandas        # installation of 🐼 from Anaconda repository
conda install pandas=1.0.1  # installation of a specific version
```
The installation packages can also be made from the default shell with the following commands:
```
conda install -n conda-env pandas   # with the environment name
conda install -p /path/to/conda-env pandas  # with the path to the environment
```
#### Packages Installations from other Conda Repositories
Using conda, it is possible to install packages from other repositories. The example below, we will install a 3rd party package from other repository from Conda-Forge, in this scenario, we need to add the flag `--channel` or `-c`
```
conda install -c conda-forge opencv   # or use --channel
```
If getting an error from above command, try to update conda with the command:
```
conda update --all
```
#### Package Installation from Pypi
This command will always look for the latest version of the package and installs it. It also searchs for the dependencies listed in the package metadata and install those dependencies to insure that the package has all the requirements it needs.

📝 [What is pip?](https://realpython.com/what-is-pip/)
```
pip install requests
```
#### Update Packages
```
conda update    # updates all the packages installed in the environment
conda update --all --yes
conda update pandas    # from the activated environment
conda update -n conda-env pandas    # with the environment name
conda update -p /path/to/conda-env pandas   # with the path to the environment
```
#### Remove Packages
```
conda remove opencv
conda remove --name conda-env opencv scipy matplotlib
```
#### Packages Management
```
conda search -f matplotlib    # search for all the available versions of a certain package
```
#### Python
```
conda search -f python     # display all available Python versions 🐍
conda install python=3.7   # install a specific python version
conda update python        # update the current Python version
where python               # show the locations of all versions of Python that are currently in the path
python --version           # show the version of the current active Python
where.exe python           # show all python libraries locations on the machine
```
#### Jupyter Notebook
```
conda install jupyter
conda install ipykernel
ipython kernel install --user --name=conda-env
conda install nb_conda    # allows easy switch between kernels in Jupyter Notebook
jupyter notebook --ip=0.0.0.0 --no-browser
jupyter notebook stop
```
#### More Commands
```
conda --version    # check conda's current version
conda update conda    # update conda in the default environment
conda update --all
conda info     # get a detailed list of information

conda env list     # display the list of conda environments. A * shows the current activated environment
conda list     # list installed packages in the current environment
pip freeze    # list all packages already installed with pip
conda list -n conda-env    # list packages installed with name
conda list -p /path/to/conda-env    # list packages installed with path
conda env export -f environment.yml    # or use --file. Make an environment file
conda env create -n conda-env -f /path/to/environment.yml   # create an environment from the environment file
conda env update -n conda-env -f /path/to/environment.yml   # update an environment with the environment file

pip install -r requirements.txt    # install multiple packages from a requirements file
conda create --clone conda-env --name conda-env-2   # make exact copy of an environment
conda list --explicit > conda-env.txt   # save environment to a text file
pip freeze > conda-env.txt    # save environment to a text file with pip
conda env create --file conda-env.txt   # create environment from a text file
pip install -r conda-env.txt    # create environment from a text file with pip

conda env remove --name conda-env   # remove environment
```
#### The sample routine
```
conda create -n conda-env python=3.7    # or use --name
conda activate conda-env
conda install pip
conda info
conda env list
conda update python
conda update --all --yes
conda install ipykernel
ipython kernel install --user --name=conda-env
conda install nb_conda  # allows easy switch between kernels in Jupyter Notebook
jupyter notebook --ip=0.0.0.0 --no-browser

pip install numpy
pip install pandas
pip install seaborn
pip install scikit-learn
pip install matplotlib

conda update --all --yes
```
#### Sources:
📝 [Conda Package Management](https://docs.conda.io/projects/conda/en/latest/index.html)
📝 [Conda Configuration](https://conda.io/projects/conda/en/latest/user-guide/configuration/index.html)
