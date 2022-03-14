# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 3: Releases and Deployments

Welcome to module 3, class 3 of this Octopus Deploy Fundamentals training course.

In this class, we'll be learning about Releases and Deployments.

First, a few definitions.

- [Releases] A Release is a snapshot of the Deployment Process at a specific time. Releases also includes a point-in-time snapshot of any associated assetts, such as any Packages, Scripts, and Variables. (Note that we'll be covering Variables in the next class, but this is important so it's appropriate to call it out now.) 
- [Deployments] When you Deploy a Release, you are executing the Deployment Process, with all the associated details, as they existed when the Release was created.

[![Link to YouTube video](https://img.youtube.com/vi/syfl59pR4ZU/0.jpg)](https://www.youtube.com/embed/syfl59pR4ZU)

### Transcript

Let's create a Release and Deployment.

[Fade to Project Overview page for RandomQuotes]

We'll be using a Project we created earlier in this module, which deploys a Package we uploaded in module 2, to the Infrastructure we configured in module 1.

[Switch tabs to default IIS page on the Deployment Target]

Before we begin, observe that our Deployment Target is currently serving the Default IIS start page. If everything goes well, by the end of this video, we'll be able to refresh this page to reveal the RandomQuotes website. 

Let's get started.

[Switch tabs back to Project Overview page for RandomQuotes]

Begin by clicking CREATE RELEASE.

[Click CREATE RELEASE]

Give the release a version number, such as 2022.3.31 or 1.0.0. Octopus Deploy expects SemVer for the Release Version. 

[Add version 2022.3.31]

Next we select the package version. We only have one version of the package to choose from, but in a real project we would probably have a new package for each CI build. By default, Octopus will assume the package with the highest semantic version. (Note, this might not be the package that was most recently created or uploaded.)

[Select the most recent package]

Optionally, you can also add Release Notes. Release Notes support markdown, so you can include links back to relevant contextual information, such as tickets, pull requests, or CI builds.

Click SAVE to create the Release.

[Add a version and some notes, click SAVE]

This brings us to the page for this Release.

The primary philosophy of Octopus Deploy is that how you deploy to dev and test, should be how you deploy to production. Releases are intended to be immutable and idempotent, meaning that regardless of any future code updates or configuration changes, a given Release should always be deployed in the same way and deliver the same result. This ensures no surprises when a Release is Deployed to Production.

On this page we can see the versions of any Packages, Variables and Artifacts that have been snapshotted in this Release.

[Show Packages, Variables and Artifacts]

We can also see a log of any relevant events related to this Release, such as Release creation and any Deployments.

[Show Deployment History]

Click the DEPLOY button, to Deploy to your first Environment.

[Click DEPLOY TO DEVELOPMENT]

Here you can select when you want to deploy this Release to this Environment. You can deploy right away, or you can schedule the Deployment for some future date and time.

[Explore scheduling options, then select "Now"]

You can choose to exclude certain steps from the Deployment. We only have one Step - it wouldn't make much sense to skip that.

[Explore "Excluded steps" but don't select any]

We'll leave accept the rest of the default options and click Deploy.

[Click DEPLOY]

Once the Deploymenthas started, you are shown a Task Summary screen. This gives you an overview of all the Steps that will run, and their status.

On the right side of the screen you can see the Release Notes provided when the Release was created. We can also see the Task History, with details such as when the task was started and who triggered it.

Clicking on the Task Log will provide further details for individual Steps. This is particularly useful when troubleshooting Deployments that are failing or taking an unusually long time.

[Click TASK LOG]

We can see even more information, by setting the Log level to Verbose.

[Set to verbose]

Congratulations, you've completed your first Deployment in Octopus Deploy! Let's see if it worked!

[Switch tabs back to the IIS start page, hit refresh, observe the RandomQuotes website]

Looking good. However, if you look carefully, you may notice a couple of unexpected details.

The website includes a footer with the version number and environment name. However, these don't exactly match the package version, release version or environment name. We haven't provided any of this information yet, so the deployment is using default values that aren't accurate.

In the next class we'll talk about how to solve this problem with Variables. Then we'll go back and refine our process to ensure the right information is displayed on the website.

Let's finish this class with a few tips for managing your own Releases and Deployments.

- [After making changes, create a new Release] Since Releases are a snapshot in time, if any part of the Deployment Process is modified, including any Variables (which we'll be covering in the next class), it's necessary to create a new Release. It's important to understand this since one of the most common mistakes people make when setting up their first Deployment Process is to change some setting, forget to create a new Release, and then get confused when it doesn't appear that the setting has been updated. In fact, everything is working exactly as intended. The Release uses the old, snapshotted configuration. Remember: after changing some project setting, always create a new Release.
- [Automate Release creation] Everything we've done in this class from the Octopus Web Interface, can be automated using the Octopus API or command line tools. One popular technique is to automate the Release creation as part of a CI build process. This ensures that release notes and versions are handled consistently and significantly reduces the administrative burden.
- [Automate Deployment Triggers] If you have an environment that's intended to be always up to date with the latest source code, you can either configure Octopus to automatically trigger Deployments to given environments as soon as new Releases are created, or you can use the API or command line to trigger an OCtopus Deployment from your build server. This ensures that your continuous integration process is consistent with your production deployments. This is simpler and safer than maintaining separate processes for build and production.

For more information about automating either Releases or Deployments, check out the Additional Resources, associated with this module.

Thank you for watching, and happy deployments!
