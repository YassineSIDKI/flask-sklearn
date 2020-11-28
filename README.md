# Continuous delivery project of a maching learning application using azure, flask and sklearn

## Introduction

In this project, you will focus on creating a continuous delivery cycle with azure pipelines, using a given code for maching learning application (that you will not develop yourself) which will be hosted in github, and azure portal to create environement on which your application will be deployed.

## Project Plan

We use for planning trello to track tasks as tickets and spreadsheet with weekly planning per year

- A link to a Trello board for the project
- A link to a spreadsheet that includes the original and final project plan>

## Prerequisites

- Have a azure account
- Have a github account

## Instructions

#### Architecture

#### Setup environment

- Create a new repository in github

- Clone this repo in azure shell

- Delete azurepipeline.yml. This file will be created later and push the code

- Check that your tests are passing localy : make all. Put output here

- Push your code to newly created github repo

- Run the project on azure app service. For that use the commande az webapp up --name "". Be sure that. Put output here

- If your project is successfuly deployed you should have the following output-like: You can return to for more information [Note the official documentation should be referred to and double checked as you setup CI/CD](https://docs.microsoft.com/en-us/azure/devops/pipelines/ecosystems/python-webapp?view=azure-devops).

- From dev azure, create a project. Put output

- Add github repo to this project. To do that you should already ssh key

- Choose the azure app service already created

- Create a pipeline for this project from azure pipelines. Choose the template "python app and stuff".

- Save and run. You can check in your github repo that azurepipelines.yml already created.

- Check that your pipelines is finished and already deployed the app

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

<TODO: A short description of how to improve the project in the future>

## Demo

<TODO: Add link Screencast on YouTube>
