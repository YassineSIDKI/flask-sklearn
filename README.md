![Python application using Github Actions](https://github.com/YassineSIDKI/flask-sklearn/workflows/Python%20application%20using%20Github%20Actions/badge.svg)

# Continuous delivery project of a maching learning application using azure, flask and sklearn

## Introduction

In this project, you will focus on creating a continuous delivery cycle with azure pipelines, using a given code for maching learning application (that you will not develop yourself) which will be hosted in github, and azure portal to create environement on which your application will be deployed.

## Project Plannig

We use for planning trello to track tasks as tickets and spreadsheet with weekly planning per year

- [A link to a Trello board for the project](https://trello.com/b/M5gD0IY3/udacity)

- [A link to a spreadsheet that includes the original and final project plan](https://docs.google.com/spreadsheets/d/1Rr-CEzN8tzZDGDlJFyEK2E43slvz5DyTLUpM4616OeA/edit#gid=1348135932)

## Prerequisites

- Have a [azure](https://azure.microsoft.com/en-us/free/) account and Azure cloud shell activated
- Have a [github](https://github.com/) account

## Architecture

![alt text](https://github.com/YassineSIDKI/flask-sklearn/blob/main/diagram.png?raw=true)

## Instructions

- Create a new github repository

- From azure cloud shell, clone this repo
  ![alt text](output)

- Push your code to the newly created github repo

- Run make setup command

- Activate virtual env python source

- Run make all
  ![alt text](make all)

- From your github repo, add new github actions workflow
  ![alt text](github actions)

- Replace <yourappname> in commands.sh then run the command ./commands.sh. The <yourappname> value is the same you will use in the file make_prediction

![alt text](azwebapp)

-

- If your project is successfuly deployed you should have the following output-like: You can return to for more information [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

home page app output

- From dev azure, create a project. Put output

- Add github repo to this project. To do that you should already ssh key

- Delete azure pipeline yaml

- Choose the azure app service already created

- Create a pipeline for this project from azure pipelines. Choose the template "python app and stuff".

- Save and run. You can check in your github repo that azurepipelines.yml already created.

- Check that your pipelines is finished and already deployed the app

- Update the script part with the followin
  make setup
  make install
  make lint

- Now to check that your continuous delivery cycle is well set, do some changes in your app. For exemple : Push this changes

- The pipeline should run automaticaly and the new app deployed should show this:

- Check also that your app is running correctly by doing a prediction. run script ./make...

```bash
udacity@Azure:~$ ./make_predict_azure_app.sh
Port: 443
{"prediction":[20.35373177134412]}
```

- You can from azure cloud shell run this command az webapp log tail to see the live logs

## Enhancements

Some improvment ideas:

- Add creation of necessary resources with terraform : resource group and webapp service
-

## Demo

<TODO: Add link Screencast on YouTube>
