---
layout: docs
title: Deploying Codewind components combined
description: Deploying all Codewind components
keywords: users, projects, Kubernetes, LDAP, user management, access management, login, deployment, pod, security, securing cloud connection, remote deployment of Codewind
duration: 5 minutes
permalink: remotedeploy-combo
type: document
parent: installoncloud
order: 2
---

## Installing a Codewind remote deployment

Codewind includes a CLI to simplify the installation process. You will find `cwctl` in your HOME directory under the path ~/.codewind/{version}

The command for installing an "all-in" deployment with a new Keycloak and new Codewind service is :

`cwctl --insecure install remote` 

and requires various flags to specify where and what to install.

### Deploying Codewind with CWCTL

1.  Open a new terminal window on your local workstation
2.  Navigate to your home directory and to the Codewind cli:

```
cd ~/.codewind/0.8.0
```

Ensure you are logged into your Kubernetes or Openshift cluster

```
$ kubectl get namespaces
```

If the command is successful you should see a list of current namespaces.  If not,  ensure you are logged into your Kubernetes or Openshift cluster.

### Determine your Cloud ingress domain

The cli command requires an ingress domain,  you can find yours based on any of the existing routes:

```
oc get routes -n default
NAME               HOST/PORT                                                                                                          PATH      SERVICES           PORT               TERMINATION   WILDCARD
registry-console   registry-console-default.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud             registry-console   registry-console   passthrough   None
```

In the above example the ingress domain needed is:

```
mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

### Running the cli command

Determine the following for your cloud deployment

* {namespace}: cwctl will create the namespace if it does not yet exist
* {kadminuser} & {kadminpass}:  Initial Keycloak administrator username and password
* {kdevuser} & {kdevpass}: A developer username and password that will be granted access to this deployment of Codewind. cwctl will create the user and add it to the realm if it does not exist.
* {ingress}: the ingress domain for your cloud environment

A complete command might look something like this :

```
./cwctl --insecure install remote \
--namespace codewind-0001 \
--krealm codewind  \
--kclient codewind \
--kadminuser admin \
--kadminpass passw0rd \
--kdevuser developer \
--kdevpass passw0rd  \
--ingress mycluster-12345-7674b4bd9abbdeea0be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

Which will:

* deploy Codewind into the `codewind-0001 `namespace
* configure Keycloak with a realm called `codewind`
* configure a client prefix of `codewind`
* create an initial Keycloak administrator user called `admin` with password `passw0rd`
* create an initial Codewind user called `developer` with password `passw0rd`
* use the ingress appropriate to the deployment environment

On running the command you should see output similar to :

```
INFO[0000] Checking namespace codewind-0001 exists
INFO[0000] Creating codewind-0001 namespace
INFO[0000] Using namespace : codewind-0001
INFO[0000] Container images :
INFO[0000] eclipse/codewind-pfe-amd64:latest
INFO[0000] eclipse/codewind-performance-amd64:latest
INFO[0000] eclipse/codewind-keycloak-amd64:latest
INFO[0000] eclipse/codewind-gatekeeper-amd64:latest
INFO[0000] Running on openshift: true
...
INFO[0156] Waiting for Codewind Gatekeeper to start on https://codewind-gatekeeper-k55333j0.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
INFO[0159] Waiting for Codewind PFE to start
INFO[0159] Codewind is available at: https://codewind-gatekeeper-k55333j0.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

Codewind has been sucessfully deployed and available.

Next step, connect your [VSCode](remotedeploy-vscode.html) or [Eclipse](remotedeploy-eclipse.html) IDE to the new Codewind deployment
