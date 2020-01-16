---
layout: docs
title: Deploying Codewind components individually
description: Deploying Codewind components individually
keywords: users, projects, Kubernetes, LDAP, user management, access management, login, deployment, pod, security, securing cloud connection, remote deployment of Codewind
duration: 5 minutes
permalink: remotedeploy-single
type: document
parent: installoncloud
order: 2
---

# Installing components individually for a Codewind remote deployment

Codewind includes a CLI to simplify the installation process. You can find the `cwctl` CLI in your HOME directory under the path `~/.codewind/{version}`.

The command for installing components individually for a remote deployment with a new Keycloak and a new Codewind service is:

`cwctl --insecure install remote` 

This command requires various flags to specify where and what to install.

## Deploying Keycloak 

1.  Open a new terminal window on your local workstation.
2.  Navigate to your home directory, and then to the Codewind CLI:

```
cd ~/.codewind/0.8.0
```

Ensure you are logged into your Kubernetes or Openshift cluster.

```
$ kubectl get namespaces
```

If the command is successful, you see a list of current namespaces.  If not, ensure that you are logged into your Kubernetes or Openshift cluster.

## Determine your Cloud ingress domain

The CLI command requires an ingress domain,  you can find yours based on any of the existing routes:

```
oc get routes -n default
NAME               HOST/PORT                                                                                                          PATH      SERVICES           PORT               TERMINATION   WILDCARD
registry-console   registry-console-default.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud             registry-console   registry-console   passthrough   None
```

In the above example the ingress domain is:

```
mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

## Deploying Authentication services (Keycloak)

Determine the following for your cloud deployment:

* {namespace}: `cwctl` creates the namespace if it does not yet exist.
* {kdevuser} & {kdevpass}: A developer username and password that will be granted access to this deployment of Codewind. `cwctl` creates the user and adds it to the realm if it does not exist.
* {ingress}: The ingress domain for your cloud environment

A complete command might look something like this:

```
./cwctl --insecure install remote \
--konly \
--namespace keycloak-0001 \
--kadminuser admin \
--kadminpass passw0rd \
--ingress mycluster-12345-7674b4bd9abbdeea0be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

Which:

* Deploys just a keycloak service into the `keycloak-0001 `namespace.
* Creates an initial Keycloak administrator user called `admin` with password `passw0rd`.
* Uses the ingress domain appropriate to the deployment environment.

On running the command you see the following example output:

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
INFO[0159] Keycloak is available at: https://codewind-keycloak-k55dxqhx.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

Keycloak has been sucessfully deployed and is available.

## Deploying a remote Codewind service

To deploy a new Codewind instance in Kubernetes, generate a user in Keycloak and configure security. You can use the CLI `cwctl` with additional options.

A complete command might look something like this:

```
./cwctl --insecure install remote \
--namespace codewind-0001 \
--krealm codewind  \
--kclient codewind \
--kadminuser admin \
--kadminpass passw0rd \
--kdevuser developer \
--kdevpass passw0rd  \
--ingress mycluster-12345-7674b4bd9abbdeea0be228236d5275c9-0001.eu-gb.containers.appdomain.cloud \
--kurl https://codewind-keycloak-k55dxqhx.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud
```

Which:

* Deploys Codewind into the `codewind-0001 `namespace.
* Configures the existing previously deployed Keycloak instance with a realm called `codewind`.
* Adds a client prefix of `codewind`.
* Creates an initial Codewind user called `developer` with password `passw0rd`.
* Uses the ingress appropriate to the deployment environment.
* And the keycloak admin credentials of `admin` with password `passw0rd`.  <-??? Adds a keycloak admin / uses the keycloak admin

Running the command, you see output similar to:

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

Codewind has been sucessfully deployed and is available.

You can re-run the command several times and each time a new Codewind deployment is generated against the existing Keycloak service. A developer must have their own Codewind instance, however they might also have more than one instances assigned to them through role-based access control which `cwctl` has setup automatically.

Make a note of the address provided : `https://codewind-gatekeeper-k55333j0.mycluster-12345-7674b4bd9abbdeea5be228236d5275c9-0001.eu-gb.containers.appdomain.cloud`   You need that for configuring your IDE in the next step.

Next step: Connect your [VSCode](remotedeploy-vscode.html) or [Eclipse](remotedeploy-eclipse.html) IDE to the new Codewind deployment
