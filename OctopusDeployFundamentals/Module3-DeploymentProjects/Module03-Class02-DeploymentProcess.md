# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 2: The Deployment Process

Welcome to module 3, class 2 of the Octopus Deploy Fundamentals training course.

This class explains how a deployment process is defined in Octopus Deploy.

We'll cover,
- The Octopus philosophy of using a consistent, repeatable processes for deployment to each environment.
- Deployment steps, specifically including the "Run a Script" and "Deploy a Package" steps.
- And the difference between built-in, community and custom step templates.

[![Link to YouTube video](https://img.youtube.com/vi/0oWRg_TxWxM/0.jpg)](https://www.youtube.com/embed/0oWRg_TxWxM)

### Transcript

Let's look at an existing deployment process.

[DEMO]

This is Octopus Samples, a public Octopus instance, with various demo projects, maintained by the team at Octopus for the community. You can access it at [samples dot octops dot app](samples.octopus.app).

Let's select the Octo Pet Shop - Raw YAML Project, from the Azure Project Group.

[SELECT OCTO PET SHOP PROJECT]

This brings us to the Overview page of the Octo Pet Shop project. On this page we see information about which versions of the software have been deployed to each Environment.

We can see the Project Deployment Process by clicking Process. 

[CLICK PROCESS]

A deployment process can be as complicated, or as simple as you like. For example, here we can see Notification steps, Manual Intervention steps and steps that execute the code deployment. In this case we are deploying a bunch of Kubernetes YAML.

Note that we use these same deployment steps to deploy to each environment. Those Kubernetes YAML steps will be executed exactly the same in Development as in Production. This builds reliability and consistency into the Deployment Process. Imagine, for example, the administrative toil of repeating the configuration for each environemt. A subtle, missed inconsistency would likely cause unanticipated problems in Production. Where there are problems, it's much better to hit them in Dev.

However, there is some flexibility. Let's imagine we're continuously deploying all source control updates to Development, but deploying significantly less frequently to Production. In this case, we don't want to drown our team with notifications about every deployment to the Development environment. Equally, it wouldn't make sense to ask the business owners or DBAs to manually approve dozens, or even hundreds, of deploys each day. 

[Highlight SCOPE]

With this in mind, the notification and approval steps have been scoped to only run for Production deployments.

Let's build a deployment process of our own.

[Switch to learn.octopus.com]

Here's the Octopus Deploy Fundamentals Project Group from Class 1, now with two Projects. Let's start by creating a simple Process for the Hello World Project.

[Click Hello World, then Process]

We add a step to our Process by clicking ADD STEP.

[Click ADD STEP]

We're presented with a selection of predefined step templates. The simplest thing we can do is execute a raw script on our deployment target. Whatever you want to do, if you can script it in PowerShell, C#, Bash or F#, you can deploy it with Octopus Deploy.

[Select Script]

Octopus provides various steps for running scripts, depending on where you host your stuff. We'll be deploying the the Windows Tentacles we configured in Module 1, so we'll select the basic "Run a Script" option.

[Click ADD]

We'll give the script a name, add any notes.

[Enter details]

Then we specify where we want to execute this script. Let's run our script on each of the Deployment Targets in each environment that have been assigned the Role RandomQuotes-WebServer.

[Enter details]

Next, we provide our script. Perhaps our scripts come from source control and has been included in a package. Alternatively, we can enter it here.

[In-line source code: Write-Output "Hello World"]

Tips:
- Include everything required to run the code. Make no assumptions about the target environment. Aim to include steps to both install and configure any dependencies. Include tests to ensure that everything is set up as expected.
- Take advantage of run conditions
