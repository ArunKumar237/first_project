# First ML project

## Requirements

1. [Github Account](https://github.com)
2. [Heroku Account](https://dashboard.heroku.com/login)
3. [VS Code IDE](https://code.visualstudio.com/download)
4. [GIT cli](https://git-scm.com/downloads)


### Step 1:

Creating conda environment in VScode or Pycharm

```
conda create -p venv python==3.7 -y
```
-p : Creating the virtual environment in current(same) folder
venv : Name of the virtual environment
-y : Stands for 'yes' to confirm the execution

### Step 2:

activating the virtual environment(venv) 

```
conda activate venv/
```

### Step 3:

creating 'requirement.txt' file to install required libraries

after creating the requirement.txt file open it, and write down the libraries you require for project.

after writing save it and run the below command in terminal

```
pip install -r requirement.txt
```

### Step 4:

Create a python file 'app.py' for Flask web application

### Step 5:

After writing the web application add the files to git.

To add files to git:
```
git add .
```
or
```
git add <filename>
```

To ignore some files adding to git:
 write the name of file/folder in '.gitignore' file

To check the git status:
```
git status
```

To check all version maintained by git:
```
git log
```

To create version/commit all changes by git:
```
git commit -m 'message'
```

To send version/changes to github:
```
git push origin main
```
origin - it is a url of git hub repositary


To check remote url of git hub repositary:
```
git remote -v
```

