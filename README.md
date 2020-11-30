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

- You can see in github actions tab a started job

![alt text](githubjob)

- run ./commands.sh from azure shell

![alt text](azwebapp)

- You can check that your project is correctly deployed by visiting the url in last output. You should see result like:

![alt text](home page screenshot)

- From dev azure, create a project.
  ![alt text](create project azure)

- Add github repo to this project. For that you should install azure pipelines in github in marketplaces (see this)
  ![alt text](azwebapp)

- Choose the azure app service already created
  ![alt text](azwebapp)

- Create a pipeline for this project from azure pipelines. Choose the template "python app and stuff".
  ![alt text](azwebapp)

- Update the script part of yaml file with the following

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

- Save and run. You can check in your github repo that azurepipelines.yml already created.
  ![alt text](azwebapp)

- Check that your pipelines is finished and already deployed the app
  ![alt text](azwebapp)

- Now to check that your continuous delivery cycle is well set, do some changes in your text app. For exemple : Push this changes

- The pipeline should run automaticaly and the new app deployed should show this:

- Check also that your app is running correctly by doing a prediction. run script ./make...

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
-

## Demo

<TODO: Add link Screencast on YouTube>
