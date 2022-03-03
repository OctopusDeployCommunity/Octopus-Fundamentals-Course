# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 1: Projects and Project Groups

Welcome to module 3, class 1 of the Octopus Deploy Fundamentals training course.

In this module we'll explain how to deploy the package we published in module 2, to the infrastructure we configured in module 1.

In class 1, we'll introduce the concepts of Projects and Project Groups.

NOTE: Replace this link with the new video!
[![Link to YouTube video](https://img.youtube.com/vi/gfaRUIlQybA/0.jpg)](https://www.youtube.com/embed/gfaRUIlQybA)

### Transcript

Projects are where you define the process for deploying your software. They are also used for managing runbooks for general operations tasks associated with that software. However, in this module we'll be focussing on deployment, rather than operations tasks.

Projects work best when they are small and focussed. It's tempting to add all the components of an application (APIs, UIs, databases etc) to a single project. However, this temptation should be avoided. We don't want to re-run database updates for every small tweak to the UI.

Instead, start by creating a Project Group for the application. Then add separate Projects to the Project Group for each component of the application. This allows each component to be managed and deployed indepenently, in-line with the single responsibility principle and a bias toward loose-coupling. Where it's desirable to deploy all the components together, we can create a coordinating Project within the same Project Group.

Let's create our first Project and Project Group.

Navigate to the Pojects page in the Octopus Deploy interface and click "ADD GROUP", enter a name and click "SAVE".

[Name is "Octopus Deploy Fundamentals Demos"]

Now click "ADD PROJECT", provide a name for this component, and click "SAVE". You've just created your first project.

[Name is "Random Quotes"]

Let's start by reviewing the settings for our Project.

On the settings page we can upload a logo for the Project, and enter a description. The description supports markdown, allowing us to hyperlink to relevant the source code, build server, documentation or whatever else you feel is relevant.

After saving the page, we can see that the image and description have been updated, including any hyperlinks.

Consider the following advice when setting up your own projects:

- [Use concise names] Use concise names. Brevity goes a long when naming projects.
- [Automate all the things] Aim to automate the deployent of every part of the system. If the website updates are automated through Octopus, but deployments are regularly blocked on manual database updates, you'll need to automate the database steps to unleash Octopus's full potential.
- [Break up big projects] If separate components of a system can be deployed independently, break them up into separate projects. Smaller projects are simpler, easier to govern and maintain, and both faster and safer to deploy.

