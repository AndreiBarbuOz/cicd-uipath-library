# AWS Codepipeline project for UiPath Library deployment

This project is a model that showcases the ideas around Continuous Integration/Continuous Deployment found in most programming languages and associated with good practices and long term positive outcomes

## Content

A CloudFormation template which creates a stack that instantiates a CodePipeline. The pipeline has the function of deploying new versions of the workflows as packages, being triggered by `git push` commands into the Source repository

## Installation

### Prerequisites

* An AWS account 
* A dockerized UiPath robot - a Docker image containing the UiPath robot and the PowerShell module for the Orchestrator API. This can be created using [dockerized-robot](https://github.com/AndreiBarbuOz/dockerized-robot)
* Access to an Orchestrator instance for Test purposes

### Configuration
* The parameters.json file need to be updated with environment values
	- RepositoryName: name of the repository where changes are tracked
	- BranchName: name of the branch that is being tracked
	- CodeBuildImageStackName: name of the cloudformation stack containing the CodeBuild image. The export name is `${CodeBuildImageStackName}-EcrUri`
	- The `Parameter Store` in the AWS account need to contain parameters needed for the Orchestrator connection


### Create the code deployment stack
```cmd
aws cloudformation create-stack --stack-name deploy-pipeline --template-body file://uipath-deploy.yaml --parameters file://parameters.json --capabilities CAPABILITY_NAMED_IAM 
``` 
