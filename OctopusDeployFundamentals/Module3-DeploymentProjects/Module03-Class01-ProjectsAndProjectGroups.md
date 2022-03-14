# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 1: Projects and Project Groups

Welcome to module 3, class 1 of this Octopus Deploy Fundamentals training course.

In this module we'll explain how to deploy the Package we uploaded in module 2, to the Infrastructure we configured in module 1.

In class 1, we'll introduce the concepts of Projects and Project Groups.

NOTE: Replace this link with the new video!
[![Link to YouTube video](https://img.youtube.com/vi/gfaRUIlQybA/0.jpg)](https://www.youtube.com/embed/gfaRUIlQybA)

### Transcript

Projects are where you define the process for deploying your software. They are also used for managing runbooks for general operations tasks associated with that software. However, in this module we'll be focussing on deployment, rather than operations tasks.

[Blank slide]

Projects work best when they are small and focussed. 

[Reveal icons for website, service and database]

Let's imagine we're looking after the accounting software for our company. It has a web portal, some background service and a database.

[Reveal monolithic project]

It's tempting to add everything to a single project. However, this temptation should be avoided. We don't want to be re-running database updates every time we tweak to the UI.

[Reveal Project group architecture, with separate mini projects for separate components]

Instead, start by creating a Project Group. Then add separate Projects to that Project Group for each component that can be deployed independently. In-line with the single responsibility principle, and a bias toward loose-coupling, this allows each part to be managed and deployed on its own schedule. 

[Add a global deployment coordinator project]

Where it's desirable to deploy everything together, we can create a coordinating Project within the same Project Group.

Let's create our first Project and Project Group.

[Fade to demo]

Navigate to the Projects page in the Octopus Deploy interface and click "ADD GROUP", enter a name and click "SAVE".

[Name is "Fundamentals Demos"]

Now click "ADD PROJECT", provide a name for this component, and click "SAVE". You've just created your first project.

[Name is "Random Quotes"]

Let's start by reviewing the settings for our Project.

On the settings page we can upload a logo for the Project, and enter a description. The description supports markdown, allowing us to add relevant hyperlinks, such as the source code, build server, documentation pages or whatever else may be useful to Project maintainers.

After saving the page, we can see that the image and description have been updated, including any hyperlinks.

Consider the following advice when setting up your own projects:

- [Use concise names] Use concise names. Brevity goes a long when naming Projects.
- [Automate all the things] Aim to automate the deployent of every part of the system. If the website updates are automated through Octopus, but deployments are regularly blocked on manual database updates, you'll want to automate the database steps to unleash Octopus's full potential.
- [Break up big projects] If separate components of a system can be deployed independently, break them up into separate projects. Smaller projects are simpler, easier to govern and maintain, and both faster and safer to deploy.

Thanks for watching, and happy deployments!
