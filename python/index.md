---
title: Python
has_children: true
---

## pip

upgrade pip: `pip install --upgrade pip`

Install per requirements.txt: `pip install -r`

Generate requirements.txt \(with strict versions\): `pip freeze > requirements.txt`

Set up to access PyPi mirror:  
`~/.pip/pip.conf`:
 ```
   [global]  
   trusted-host = mirrors.tuna.tsinghua.edu.cn  
   index-url = https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
   extra-index-url =   
```

## Virtual Environment

Activate: `source <path to venv>/bin/activate`. This sets environmental variables, particularly:

* `PATH` \(`<venv>/bin/`\)
* `VIRTUAL_ENV` \(`<venv>/`\)

Run in a virtual environment without activating it: `<path to venv>bin/python <optional command or executable>`

## Pandas

Read whitespace delimited file:  
`read_csv('file.csv', delim_whitespace=True)`

## To Organize

Python 3 virtual environment:
```
  virtualenv -p python3 venv-  
  source -project/bin/activate  
```

pexpect and paramiko  
shell / SSH interaction via Python object

Look up Celery tasks in Python

String similarity  
`levenshtein`

Capture result of most recent expression statement: _
IPython / Jupyter:
Useful for:
Exploratory work (scientific development, troubleshooting)
Remote access for:
Notebook, IPython console, terminal, file browser
For issue tickets
Capturing state (API calls, etc)
Documenting remediation steps
---
Install: `pip install jupyterlab`  # In virtual environment
Access output from history:
`Out[<number>]`  # See: In[<number>] as interpreted.
Context help:
`<object>?`
Run a script: `%run`
Launch an editor: `%edit`
Run a system command: `!<command>`
Kernels:
Prepare virtual environment for use in Jupyter (from within virtual environment):
```
			python -m ipykernel install \
				--name <env-name> \
				--display-name "<env-display-name>"
				--prefix=$DIRECTORY
```
		Add virtual environment to Jupyter (from within server environment):
			`jupyter kernelspec install $DIRECTORY/jupyter/kernels/<env-name>`
		*** Look into support for other languages through Jupyter kernels (Julia, R, Bash, etc)

pip install from git repo and branch:
https://stackoverflow.com/questions/20101834/pip-install-from-git-repo-branch

Python detect venv:
https://stackoverflow.com/questions/1871549/determine-if-python-is-running-inside-virtualenv
```
		import sys
		def is_venv():
		    return (hasattr(sys, 'real_prefix') or
		            (hasattr(sys, 'base_prefix') and sys.base_prefix != sys.prefix))
```
		The check for `sys.real_prefix` covers `virtualenv`, the equality of non-empty `sys.base_prefix` with `sys.prefix` covers `venv`.

Install local package, updating with changes:
`pip install -e <my_device_repo> -c  <my_device_repo>/contraints.txt`
# `-e` is Editable mode

pip syntax for git with branch or tag and egg:
`git+https://github.com/<owner>/<repo>.git@<branch-or-tag>#egg=<name-from-setup.py>`

Troubleshoot insecure pip download:
Unverified HTTPS request is being made. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings

How to source from a mirror in devpi? (does it just use pip.conf?)
https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple
for performance in China
https://developer.download.nvidia.com/compute/redist/jp/v42/
for tensorflow-gpu
https://pypi.python.org/simple
if not found elsewhere

Interesting
https://stackoverflow.com/questions/293431/python-object-deleting-itself

python
Checkout bypthon REPL

For loop over list
Removing / adding items can cause elements to be skipped in loop 