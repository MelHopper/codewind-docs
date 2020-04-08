---
layout: docs
title: Deploying Codewind remotely
description: Deploying Codewind remotely
keywords: users, projects, Kubernetes, LDAP, user management, access management, login, deployment, pod, security, securing cloud connection, remote deployment of Codewind
duration: 5 minutes
permalink: remote-deploying-codewind
type: document
---

# Deploying Codewind remotely

Codewind can be used in one of three ways - locally, [hosted](./che-installinfo.html) as an application on a cloud, or remotely. By deploying Codewind remotely, you can develop your code locally, but build and run your application in the cloud. Remote use of Codewind frees up desktop resources, using the cloud's resources to build and run applications. 

To learn how to use Codewind once it has been deployed remotely, see [Using Codewind remotely](remote-codewind-overview.html).

## What you will learn

You will learn how to deploy Codewind to be used remotely. 

After you install your local IDE and configure Codewind for local use, you will:

1. Install the Codewind operator in your cloud.
2. Deploy your Codewind instances. 

Finally, you will learn how to remove a remote deployment of Codewind.

## Prerequisites

Before deploying Codewind to the cloud, you must:

1. **Install your preferred IDE on your local machine.** For more information about installing Eclipse, see [Getting started with Codewind for Eclipse](eclipse-getting-started.html), or for more information about installing VS Code, see [Getting started with Codewind for VS Code](vsc-getting-started.html).

2. **Have an active Kubernetes context and log in to the cluster.** Codewind can run in OpenShift 3.11, OpenShift 4.3, OpenShift in IBM Public Cloud, standalone Kubernetes, and Kubernetes in Docker.

3. **For Linux desktop, ensure your workstation is set up to use a Keyring.** An example of a Keyring on Linux is Secret Service. 


<!-->
1. git clone codewind-operator
2. install keycloak (install.sh keycloak)
3. Add Jane to keycloak (copy section from codewind-operator readme. Not a link)
4. install Codewind (install.sh codewind). No readme link
-->


## 1. Clone the Codewind operator repository

The Codewind operator helps with the deployment of Codewind instances in an Openshift or Kubernetes cluster. Installing the Codewind operator is usually performed by your system administrator. 

Clone the Codewind operator repository, for example: 

`$ git clone https://github.com/eclipse/codewind-operator`

## 2. Install Keycloak

Use the `install.sh` script in the Codewind operator repository to install Keycloak into your cluster: 

`$ install.sh keycloak`

## 3. Add a new user to Keycloak

1\. Ensure that the Realm is set to `Codewind` by clicking on the dropdown arrow on the page. Select **Codewind** if necessary, then:
    1. Click **Users**.
    2. Click **Add user**.
    3. Complete the **username** field.
    4. Complete the **email**, **Firstname**, and **Lastname** fields as required.
    5. Ensure **user enabled** is **On**.
    6. Click **Save**.

2\. Assign an initial password to the user account by clicking **Credentials** and then add the initial password.

3\. The field **Temporary = On** requires users to change their passwords during first connection. Set **Temporary = Off** makes this password valid for continuous use and not require changing on first connect.

4\. Click **Set Password** to save changes. Log out of the Keycloak admin page.

_MG: Do we need the `Updating the Keycloak password in the operator secret` section in here also?_

## 4. Deploy a Codewind instance

Use the `install.sh` script in the Codewind operator repository to deploy a Codewind instance:

`$ install.sh codewind`

## Next steps

You have now finished installing the Codewind operator, and you have deployed a Codewind instance.

In the next topic, you will learn how to [use Codewind remotely](./remote-codewind-overview.html).
