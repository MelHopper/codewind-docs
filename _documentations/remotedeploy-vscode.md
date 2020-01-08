---
layout: docs
title: Connecting VSCode to Remote Codewind
description: Connecting a VSCode IDE to a Remote Codewind deployment
keywords: users, projects, Kubernetes, LDAP, user management, access management, login, deployment, pod, security, securing cloud connection, remote deployment of Codewind
duration: 5 minutes
permalink: remotedeploy-vscode
type: document
parent: installoncloud
order: 2
---

## Connecting VSCode to Remote Codewind

Locate the Codewind view in VSCode and click the cloud icon to launch the new connection wizard:

![New Connection](./images/remotevs/newConnection.png)

Add a connection name and press enter

![Name Connection](./images/remotevs/connectionName.png)

Complete the 3 required fields and save : Gatekeeper URL,  developer username, develper password:

![Required Fields](./images/remotevs/connectionCreds.png)

The IDE will then validate the connection and add it to the Codewind panel :

![Validate settings](./images/remotevs/connectionAdded.png)

At this the IDE and Codewind are connected

## Adding a deployment registry

Before projects can be deployed on Kubernetes you need to specify a docker registry. In this example we will use DockerHub.  If its not already open navigate to the connection details page via the link :

![Docker Registry](./images/remotevs/connectionSettings.png)

Locate and click 'Open Container Registry Manager':

![Open Registry Manager](./images/remotevs/registryManager.png)

Once the image registry screen opens click '+ Add New'

![Adding registry](./images/remotevs/ImageRegistries.png)

Then complete the docker connection details for example if you are using Docker hub enter docker.io and press enter

![New Registry](./images/remotevs/newReg1.png)

Then enter

1. your dockerhub username
2. your dockerhub password
3. your repo name which is usually the same as your username

The connection will be tested to validate your credentials and stored in a Kubernetes secret within the Codewind service.

## Create a new project

Navigate to the Codewind panel and click the + icon beside the new cloud deployment :

![Adding new remote project](./images/remotevs/newProject.png)

Select the template type, project name and your new project should be built and after a few seconds begin running in the cloud.


## Copying an existing local project to the cloud

Copying an existing local project "myFirstNodeProject" over to the remote Codewind deployment.

To begin :

Select the remote deployment and click the "Add existing project button"

![Add existing project](./images/remotevs/addExistingProject.png)

Navigate to the folder containing the local project files and click "Add to Codewind":

![Add to Codewind](./images/remotevs/existingProject.png)

Codewind will ask you to confirm the project type identified as NodeJS:

![Confirm Project Type](./images/remotevs/confirmProjectType.png)

click Yes

The project files are copied over to the Codewind server and the new "myFirstNodeProject" appears in the Codewind panel:

![Project Added](./images/remotevs/projectAdded.png)

Codewind will begin building the code and Docker image, moments later the Project Image will be uploaded to DockerHub and used by your cloud deployment to provision a new pod. 

![Build Success](./images/remotevs/buildSuccess.png)

`myFirstProject` on `MyIBMCloud` is now running and ready.

Congratulations, In this topic you:

1. Deployed a new Codewind install into Openshift
2. Configured your IDE to use this new deployment
3. Registered all the necessary security parameters
4. Created a new project built that builds and runs in the cloud
5. Copied an existing local project to build and run in the cloud

In the next step you will learn how to remove an existing Codewind deployment

[Remove a remote deployment of Codewind](./remote-removing.html)