# AWS Codepipeline project for UiPath Library deployment

This project is a model that showcases the ideas around Continuous Integration/Continuous Deployment found in most programming languages and associated with good practices and long term positive outcomes

## Content

A CloudFormation template which creates a stack that instantiates a CodePipeline. The pipeline has the function of deploying new versions of the workflows as packages, being triggered by `git push` commands into the Source repository

## Prerequisites

* An AWS account 
* A dockerized UiPath robot - a Docker image containing the UiPath robot and the PowerShell module for the Orchestrator API. This can be created using [dockerized-robot](AndreiBarbuOz/dockerized-robot)
* Access to an Orchestrator instance for Test purposes
* It is assumed that the 

__The `docker-image-repository` stack also creates a Role which should be assumed by the EC2 Instance which builds the Docker container__


For easy use of `build-image.ps1` it is recommended that the actual docker image is performed on an EC2 instance. In this case, the Role created by the stack should be assigned to the EC2 instance, to be assumed at runtime.
```cmd
 powershell -file build-image.ps1
```

### Create the code deployment stack
```cmd
aws cloudformation create-stack --stack-name deploy-pipeline --template-body file://pipeline-deploy//uipath-deploy.yaml --parameters file://pipeline-deploy//parameters.json --capabilities CAPABILITY_NAMED_IAM 
``` 
