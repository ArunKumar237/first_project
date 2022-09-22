# Basic CI/CD Pipeline

## Requirements

1. [Github Account](https://github.com)
2. [Heroku Account](https://dashboard.heroku.com/login)
3. [VS Code IDE](https://code.visualstudio.com/download)
4. [GIT cli](https://git-scm.com/downloads)

### Step 1: Creating Project folder in GitHub Repositary:

Login to GitHub and create a Project folder with 'Name', 'Readme file', '.gitignore' and license
Clone it to local machine using git clone method 
```
git clone <github url of the project folder>
```

### Step 2: Virtual environment creation:

Creating conda environment in VScode or Pycharm

```
conda create -p venv python==3.7 -y
```
-p : Creating the virtual environment in current(same) folder
venv : Name of the virtual environment
-y : Stands for 'yes' to confirm the execution

### Step 3: activating the virtual environment(venv) 

```
conda activate venv/
```

### Step 4: Installing libraries:

creating 'requirement.txt' file to install required libraries

after creating the requirement.txt file open it, and write down the libraries you require for project.

after writing save it and run the below command in terminal

```
pip install -r requirement.txt
```

### Step 5: Creating Flask web app:

Create a python file 'app.py' for Flask web application

### Step 6: Pushing code using Git:

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

### Step 6: Creating Docker Container and Testing

Create a docker file with name 'Dockerfile'

BUILD DOCKER IMAGE:
```
docker build -t <image_name>:<tagname> .
```
>Note: Image name for docker file must be in lower case


To list the docker images:
```
docker images
```


To Run the image
```
docker run -p 5000:5000 -e PORT=5000 <Image ID>
```


To check running container in docker:
```
docker ps
```

To stop docker container:
```
docker stop <container ID>
```


### Step 7: Heroku deployment

To setup CI/CD pipeline in heroku we need 3 information:
```    
1. Heroku email id:
2. Heroku api key: available in account section
3. Heroku app name: name of your app
```

1. Create folder with name '.github' in project folder
2. Create another folder in the '.github' folder with name 'workflows'.
3. In the folder 'workflows', create a file name called 'main.yaml'. in this main.yaml file write this code and do changes as required
```
# Your workflow name.
name: Deploy to heroku.

# Run workflow on every push to main branch.
on:
  push:
    branches: [main]

# Your workflows jobs.
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # Check-out your repository.
      - name: Checkout
        uses: actions/checkout@v2


### ⬇ IMPORTANT PART ⬇ ###

      - name: Build, Push and Release a Docker container to Heroku. # Your custom step name
        uses: gonuit/heroku-docker-deploy@v1.3.3 # GitHub action name (leave it as it is).
        with:
          # Below you must provide variables for your Heroku app.

          # The email address associated with your Heroku account.
          # If you don't want to use repository secrets (which is recommended) you can do:
          # email: my.email@example.com
          email: ${{ secrets.HEROKU_EMAIL }}
          
          # Heroku API key associated with provided user's email.
          # Api Key is available under your Heroku account settings.
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          
          # Name of the heroku application to which the build is to be sent.
          heroku_app_name: ${{ secrets.HEROKU_APP_NAME }}

          # (Optional, default: "./")
          # Dockerfile directory.
          # For example, if you have a Dockerfile in the root of your project, leave it as follows:
          dockerfile_directory: ./

          # (Optional, default: "Dockerfile")
          # Dockerfile name.
          dockerfile_name: Dockerfile

          # (Optional, default: "")
          # Additional options of docker build command.
          docker_options: "--no-cache"

          # (Optional, default: "web")
          # Select the process type for which you want the docker container to be uploaded.
          # By default, this argument is set to "web".
          # For more information look at https://devcenter.heroku.com/articles/process-model
          process_type: web
          
   
          
### ⬆ IMPORTANT PART ⬆ ###
```
4. Go to > current Project folder in github > settings > secrets > actions > New repository secret.

5. After getting into New repository secret tab, fill the Name and Heroku_email in value and save the secret.
repeat this for API key as well as App name (should be same as Heroku app_name).

6. Go to > 'Actions' in Project folder > re-run all jobs


Well Done your CI/CD pipeline is ready to use
