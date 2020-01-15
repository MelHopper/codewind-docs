---
layout: docs
title: "Getting started with Codewind for VS Code"
description: "Getting started with Codewind for VS Code"
keywords: introducing, introduction, overview, tools, get, getting, start, started, install, vscode, visual, studio, code, Codewind for VS Code getting started, VS Code Marketplace, VS Code Extensions view, VS Code workspace,installing Codewind for VS Code
duration: 1 minute
permalink: vsc-codechange
type: document
order: 1
parent: mdt-vsc-overview
---
# Making a code change
<br/>
Codewind automatically builds and redeploys your application whenever you make a code change and save the file.

To see this in action, we can make a change to the getting started example.

First step is to edit the index.html file

![](dist/images/vsc-codechange.png){:width="800px"}

and navigate to the bottom of the file to find the lines

![](dist/images/vsc-codeline.png)

Change the heading from *Congratulations* to be *I did this* 

![](dist/images/vsc-ididthis.png)

You will see the status of the project change to be *stopped* whilst the project is being rebuilt and deployed

![](dist/images/vsc-buildstopped.png)

After a few moments, the status will change back to running

![](dist/images/vsc-buildrunning.png)

Clicking the
![](dist/images/launchicon.png)
icon will now show your code change running

![](dist/images/vsc-screenchanged.png)

Next step: [Buiding and deploying in a cloud environment](remoteoverview.html)
