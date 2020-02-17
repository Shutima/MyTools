# How to create Virtual Environment with pipenv
This document describe how to use pipenv to create virtual environment

## Getting Started
Python should be installed on the system: https://www.python.org/downloads/

## Pipenv Introduction
First, let's install pipenv
```
pip install pipenv
```
**Note:** After installing pipenv, we can forget about `pip` because pipenv acts as a replacement for `pip`. Pipenv also introduces 2 files:
1. **Pipfile:** Replacing `requirements.txt`
2. **Pipfile.lock:** which allows deterministic builds
Pipenv uses `pip` and `virtualenv` under the hood but simplifies their usage with a single command line interface
### Creating Virtual Environment Using pipenv
When creating a new Python application, we need to first spawn a shell in a virtual environment to isolate the development of this application. 
```
pipenv shell
```
This command will create a virtual environment. It will create a virtual environment at: `%USERPROFILE%\.virtualenvs\[name_of-env]`
![pipenv1](https://user-images.githubusercontent.com/57285863/74615670-30a44a80-5123-11ea-8981-853e8693ce76.png)

![pipenv2](https://user-images.githubusercontent.com/57285863/74615730-824cd500-5123-11ea-9500-191eaf27d9e3.png)
**Tip:** If you want to create a virtual environment with a more specific version of Python by providing a `--python` argument with a specific version such as: `--python 3.6`
### Installing 3rd Party Package Inside the Virtual Environment
This command will install `flask` inside the virtual environment with a specific version.
```
pipenv install flask==0.12.1
```
This will also create `Pipfile` and `Pipfile.lock` if not already created
![pipenv3](https://user-images.githubusercontent.com/57285863/74615956-49adfb00-5125-11ea-9f9f-a4b486a9a78c.png)

![pipenv4](https://user-images.githubusercontent.com/57285863/74615964-54689000-5125-11ea-8667-5b91ad6414b7.png)

Now, let's install another 3rd party application inside this virtual environment.
```
pipenv install numpy
```
You can also install a package directly from a version control system (VCS). This can be done by specifying the locations just like how we do it in `pip`. For example, this command below will install `requests` library from version control:
```
pipenv install -e git+https://github.com/requests/requests.git#egg=requests
```
Now for an application, you will need some unit tests. And, you want to use Python to run these unit tests. So, you need to install `pytest` but NOT in production. This can be done by specifying that this dependency is only for development with `--dev` argument:
```
pipenv install pytest --dev
```
By adding the argument `--dev`, this will put the dependency in a special `[dev-packages]` location in the `Pipfile`. These development packages only get installed if you specify `--dev` argument with `pipenv install`

Once your application works on local development environment. It is time to push it to production. Before doing so, you need to lock your environment so you can ensure you have the same one in production:
```
pipenv lock
```
This will update the `Pipfile.lock`, which you will never need do edit manually.
Now, once you get your code and `Pipfile.lock` in your production environment, you should install the last successful environment recorded:
```
pipenv install --ignore-pipfile
```
This command tells pipenv to ignore `Pipfile` for installation and use what's in `Pipfile.lock`.
Given this `Pipfile.lock`, pipenv will create the exact same environment you had when you ran `pipenv lock`, sub-dependencies and all.

### Building the Same Virtual Environment for Another Developer
When another developer would like to add some code in your application, they would get the code, including `Pipfile` then use this command:
```
pipenv install --dev
```
This commands will install all the dependencies needed for development.
```
**Important Note**
When an exact version isn’t specified in the Pipfile, the install command gives the opportunity for dependencies (and sub-dependencies) to update their versions.
```
### Some Useful Pipenv commands
Display a dependency graph to understand your top-level dependencies and their sub-dependencies:
```
pipenv graph
```
This command will print out the three-like structure showing your dependencies. For example:
```
Flask==0.12.1
  - click [required: >=2.0, installed: 7.0]
  - itsdangerous [required: >=0.21, installed: 1.1.0]
  - Jinja2 [required: >=2.4, installed: 2.11.1]
    - MarkupSafe [required: >=0.23, installed: 1.1.1]
  - Werkzeug [required: >=0.7, installed: 1.0.0]
numpy==1.18.1
pytest==5.3.5
  - atomicwrites [required: >=1.0, installed: 1.3.0]
  - attrs [required: >=17.4.0, installed: 19.3.0]
  - colorama [required: Any, installed: 0.4.3]
  - more-itertools [required: >=4.0.0, installed: 8.2.0]
  - packaging [required: Any, installed: 20.1]
    - pyparsing [required: >=2.0.2, installed: 2.4.6]
    - six [required: Any, installed: 1.14.0]
  - pluggy [required: >=0.12,<1.0, installed: 0.13.1]
  - py [required: >=1.5.0, installed: 1.8.1]
  - wcwidth [required: Any, installed: 0.1.8]
requests==2.22.0
  - certifi [required: >=2017.4.17, installed: 2019.11.28]
  - chardet [required: >=3.0.2,<3.1.0, installed: 3.0.4]
  - idna [required: >=2.5,<2.9, installed: 2.8]
  - urllib3 [required: >=1.21.1,<1.26,!=1.25.1,!=1.25.0, installed: 1.25.8]
```
Additionally, you can also reverse the tree to show the sub-dependencies with the parent that requires it:
```
pipenv graph --reverse
```
## The Pipfile
`Pipfile` is intended to replaced `requirements.txt`.
This file is sepearated into sections:
1. `[dev-packages]` for development-only packages
2. `[packages]` for minimally required packages
3. `[requires]` for othe requirements like a specific version of Python
```
[[source]]
name = "pypi"
url = "https://pypi.org/simple"
verify_ssl = true

[dev-packages]
pytest = "*"

[packages]
flask = "==0.12.1"
numpy = "*"
requests = {editable = true,git = "https://github.com/requests/requests.git"}

[requires]
python_version = "3.8"
```
## The Piplock.file
This file enables deterministic builds by specifying the exact requirements for reproducing an environment. It contains the exact version of packages and hashes to support more secure verification. The syntax of this file is JSON.

## Pipenv Extra Features
Open 3rd party package in your default editor:
```
pipenv open flask
```
Run command in the virtual environment without launching a shell:
```
pipenv run <insert command here>
```
```
pipenv check   # Check for security vulnerabilities in your ENV
pipenv uninstall numpy   # Install unwanted package
pipenv uninstall --all   # Uninstall all packages from your ENV
pipenv --venv   # Display the location of the ENV
pipenv --where  # Display the project home
```
📌 [Read more about Pipenv Guide and Package Distribution](https://realpython.com/pipenv-guide/)
