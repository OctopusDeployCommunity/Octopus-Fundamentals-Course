# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 2: The Deployment Process

Welcome to module 3, class 2 of this Octopus Deploy Fundamentals training course.

This class explains how a deployment process is defined in Octopus Deploy.

We'll cover,
- [A consistent, repeatable deployment process] The Octopus philosophy of using a consistent, repeatable processes for deployment to each environment.
- [Steps /Run a Script /Deploy a Package] Deployment steps, specifically including the "Run a Script" and "Deploy a Package" steps.
- [Built-in vs Community Step Templates] And the difference between built-in and community step templates.

[![Link to YouTube video](https://img.youtube.com/vi/0oWRg_TxWxM/0.jpg)](https://www.youtube.com/embed/0oWRg_TxWxM)

### Transcript

Let's look at an existing deployment process.

[DEMO]

This is Octopus Samples, a public Octopus instance, with various demo projects to explore. You can access it at [samples dot octopus dot app](samples.octopus.app).

Let's select the "Octo Pet Shop - Raw YAML" Project, from the "Azure" Project Group.

[SELECT OCTO PET SHOP PROJECT]

This brings us to the Overview page of the Octo Pet Shop project. On this page we see information about which versions of the software have been deployed to each Environment.

We can see the Project Deployment Process by clicking Process. 

[CLICK PROCESS]

A deployment process can be as complicated, or as simple as you like. For example, here we can see Notification steps, Manual Intervention steps and steps that execute the code deployment - in this case deploying a bunch of Kubernetes YAML.

Note that we use the same steps when deploying to each environment. Those Kubernetes YAML steps will be executed exactly the same way in Development as in Production. This is consistent with the "Build Once, Deploy Many Times" mantra, building reliability and consistency into the Deployment Process. Imagine, for example, the administrative toil of duplicating the configuration for each environment. A subtle, missed inconsistency between development and production could easily cause unexpected problems.

However, while the same steps generally get deployed consistently to all environments, there is some flexibility. Let's imagine we're continuously deploying every source control update to Development, but we're deploying significantly less frequently to Production. In this case, we don't want to drown our team with notifications about every deployment to the Development environment. Equally, it wouldn't make sense to ask the business owners or DBAs to manually approve dozens, or even hundreds, of deploys each day. 

[Highlight SCOPE]

With this in mind, the notification and approval steps have been scoped to only run for Production deployments.

Let's build a deployment process of our own.

[Switch to learn.octopus.com]

Here's the Fundamentals demos Project Group from Class 1, now with two Projects. Let's start by creating a simple Process for the Hello World Project.

[Click Hello World, then Process]

We add a step to our Process by clicking ADD STEP.

[Click ADD STEP]

We're presented with a selection of predefined Step Templates. The simplest thing we can do is execute a raw script on our deployment target. Whatever you want to do, if you can script it in PowerShell, Bash, C#, or F#, you can deploy it with Octopus Deploy.

[Select Script]

Octopus provides various Step Templates for running scripts, depending on where you host your stuff. We'll be deploying to Windows Tentacles similar to those we configured in Module 1, so we'll select the basic "Run a Script" Template.

[Click ADD]

We'll give the script a name and add some notes.

[
Name: Execute Hello World script
Description: A simple Hello World PowerShell script
]

Then we specify where we want to execute this script. Let's run our script on each of the Deployment Targets in each environment that have been assigned the Role HelloWorld-Win2019. Note that if I was using a self-hosted Octopus instance, I'd additionally have an option to run the script on the Octopus Server itself, potentially avoiding the need to set up any specific infrastructure for what might be a simple and low-risk script.

[Enter details]

Next, we provide the script that we want to execute. Perhaps our script comes from source control and has been included in a package. Alternatively, we can add the script here.

[In-line source code: Write-Output "Hello World"]

Finally, we can configure various Conditions. For example, this is where we specify whether we want the step to run for all Environments, whether the step should run if preious steps have failed, and whether users should be able to manually skip this step when triggering a deployment. We'll leave the defaults as they are for now and click SAVE.

[Click SAVE]

We've successfully created our first Deployment Process! We'll run the deployment in the next class, but first, let's build another, more interesting Process.

[Open the RandomQuotes Project]

We're going to use this Project to deploy the RandomQuotes package we uploaded in module 2, to our Infrastructure we configured module 1.

[Click Process / ADD STEP]

This time we'll look through the "Package" Step Templates and select Deploy to IIS.

[Select Package and hover over Deploy to IIS] 

Before adding this Step, let's take a moment to observe that this Step Template is maintained by the team at Octopus. Octopus provides a large selection of the most popular Step Templates out of the box. For example, there are similar steps here for deploying packages to NGINX, Azure and AWS.

In addition to the built-in step templates, Octopus also maintains a community Step Template Library. Many Octopus users and partners have shared their own Step Templates. For example, perhaps you want to deploy an AWS Lambda Function, or you'd like to use Chocolatey to ensure some dependency was installed on the Deployment Target, well, someone's already scripted those tasks and shared a Template with the community. You can explore all community Step Templates, including the source code, at [Library dot Octopus dot com](https://library.octopus.com/listing). 

[Fade to Library.Octopus.com]

If you would like to learn more about using community Step Templates, or even contributing your own, you'll find more information in the additional resources associated with this module.

[Fade back to demo] 

Let's add that Deploy to IIS step.

[Add the Deploy to IIS Step]

Once again, we can give our Step a name and add some notes.

[Add name, add notes]

This Step Template needs to be executed on Deployment Targets, and we want it to run on all the targets with the role RandomQuotes-WebServer.

[Add role]

Now we provide the package details. In Module 2 we uploaded a package to the built-in feed. Octopus interpreted the Package ID and version number from the file name of the package. We can search for the Package ID here.

[Select RandomQuotes package from builtin feed]

Next we provide various IIS configuration details. 

We're deploying an IIS Website, called RandomQuotes, we'll accept the default physical path and we want to start the website once we're done.

[Fill in those details]

We're going to set the Application Pool to use the same name, RandomQuotes, and we'll accept the default bindings.

[Fill in Application Pool and bindings section]

Since this is only a demo, we'll enable Anonymous Authentication.

[Enable Anon Auth]

Next come a couple of more advanced features. We'll cover .NET Configuration Variables in an upcoming video, so for now, we'll deselect those.

[Deselect .NET Configuration Variables]

Octopus supports .NET Configuration Transforms out of the box. By selecting this option, if your project includes transformation files in the form either star dot release dot config, or "EnvironmentName" dot release dot config, these configuration transformations will be run during deployment.

We can toggle on or off further additional features by selecting the Configure Features button.

[Select Configure Features, leave defaults, click OK]

Finally, like in our Hello World example, we can set our Run Conditions. We'll accept the defaults and hit SAVE.

[Accept default, Save]

And we're done. We've added a Step to our Process to deploy our RandomQuotes package from module 2, to the Infrastructure we configured in module 1. In the next class we'll run our first deployment! 

Remember:

- [Avoid assumptions] When creating your deployment process, don't make any assumptions about your target environment. Aim to include steps to install and configure any dependencies. Or, at the very least, verify that those dependencies have already been pre-intalled and set up appropriately.
- [Include smoke tests] After any Steps that deploy your code, add Steps to execute some smoke tests to verify that everything is set up and working as expected.
- [Use Run conditions] Take advantage of run conditions to toggle which steps are executed in each environment. It's far easier to maintain a single process that can be deployed to all environments, than it is to maintain separate processes for deploying to different environments.  

Thanks for watching, and happy deployments!