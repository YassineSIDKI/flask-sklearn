![Python application using Github Actions](https://github.com/YassineSIDKI/flask-sklearn/workflows/Python%20application%20using%20Github%20Actions/badge.svg)

# Continuous delivery for ML Flask and Sklearn project using Azure

## Introduction

In this project, you will focus on creating a continuous delivery cycle with azure pipelines, using a given code for maching learning application (that you will not develop yourself), and azure portal to create environement on which your application will be deployed.

## Project Plannig

We use for planning trello to track tasks as tickets and spreadsheet with weekly planning per year

- [A link to a Trello board for the project](https://trello.com/b/M5gD0IY3/udacity)

- [A link to a spreadsheet that includes the original and final project plan](https://docs.google.com/spreadsheets/d/1Rr-CEzN8tzZDGDlJFyEK2E43slvz5DyTLUpM4616OeA/edit#gid=1348135932)

## Prerequisites

- Have a [azure](https://azure.microsoft.com/en-us/free/) account and Azure cloud shell activated
- Have a [github](https://github.com/) account

## Architecture

![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/diagram-v2.png?raw=true)

## Instructions

- Create a new github repository

- From azure cloud shell, clone this repo
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/clonerepo.png?raw=true)

- You can run this command to check that the Makefile commands working. If you face some error during locust install, check that you have python version >=3.6

```
make setup && source ~/.udacity-devops/bin/activate && make all
```

- Delete all .yml files and change the <yourAppName> in `make_predict_azure_app.sh` and `commands.sh` by name you will give to your web app. It should be the same name in both files. Then push the project to github repo

- From your github repo, add new github actions workflow
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/githubactions.png?raw=true)

- Choose Python application workflow and change the `jobs` part in yaml file with the following

```
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.7
      uses: actions/setup-python@v2
      with:
        python-version: 3.7
    - name: Setup environrmrnet
      run: |
        make setup
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pytest
      run: |
        make lint
    - name: Test with locust
      run: |
        make test
```

- After you save and run, you can see in github actions tab a job running
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/jobgithub.png?raw=true)

- To create azure webapp service, from azure shell run `./commands.sh` from root folder
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/az%20webapp.png?raw=true)

- You can check that your project is correctly deployed by visiting the URL figured in output. You should see result like:
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/homepage.png?raw=true)

- From dev azure, create a project.
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/createprojectazure1.png?raw=true)

  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/createprojectazure2.png?raw=true)

![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/createprojectazure3.png?raw=true)

- Add github repo to this project and choose your repo
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/azurerepo.png?raw=true)

  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/azurepipelinesRepoGithub.png?raw=true)

- Choose the azure app service already created
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/choosesubscription.png?raw=true)

  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/choosewebapp.png?raw=true)

- Create a pipeline for this project from azure pipelines. Choose the template "python app and stuff".
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/azurepipelines.png?raw=true)

  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/choosewebapp.png?raw=true)

- Update the script part of yaml file with the following
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/azurepipelinesyaml.png?raw=true)

```
        - script: make setup
            workingDirectory: $(projectRoot)
            displayName: "setup virtual env"

          - script: make install
            workingDirectory: $(projectRoot)
            displayName: "Install requirements"

          - script: make lint
            workingDirectory: $(projectRoot)
            displayName: "lint"

          - script: make test
            workingDirectory: $(projectRoot)
            displayName: "load testing"

```

- Save and run. You can check in your github that azurepipelines.yml already created.

- Check that your pipelines is finished and already deployed the app
  ![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/screens/azurepipelinesrunnning.png?raw=true)

- Good news : Your continuous delivery cycle is set. To check that your continuous delivery cycle is well set, do some changes in your app.py and push.
  Replace this

```
@app.route("/")
def home():
    html = "<h3>Sklearn Prediction Home</h3>"
    return html.format(format)
```

by this

```
@app.route("/")
def home():
    html = "<h3>Sklearn Prediction Home - change to trigger pipeline</h3>"
    return html.format(format)
```

- The pipeline should run automaticaly and the deployment is done successfuly. Check the app url and check the home page. You should get this result

![alt text]()

- from azure shell, run the command and check the result

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

- You can from azure cloud shell run this command az webapp log tail to see the live logs and run make then see logs

## Enhancements

Some improvment ideas:

- Add terrafom file to create needed resources in case we want to use specific resource group for example
- Add different environments : dev, qa and prod

## Demo

<TODO: Add link Screencast on YouTube>
