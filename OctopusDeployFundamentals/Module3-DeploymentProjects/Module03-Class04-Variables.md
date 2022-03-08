# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)

### Class 4: Variables

Welcome to module 3, class 4 of this Octopus Deploy Fundamentals training course. This class is about Variables.

So far in this module we've already set up a couple of Projects and we've successfully deployed a sample website. Along the way, we explained that Octopus believes in using consistent deployment processes to each Environment. It's simpler and safer to re-use the same Packages and Processes for Deployments to development and production.

However, often there are important differences that need to be accounted for. For example, perhaps we need to use a different database connection string in different Environments. Or perhaps we need to provide some sensitive information, such as a password, that we don't want to keep in source control.

Variables solve this problem by enabling us to pass either plaintext or encrypted values to our Deployment Processes and Runbooks, at Deployment time.

In this class, we'll talk about:

- [Scoping] Scoping variables so that we can feed different values in different contexts.
- [System Variables] Using the built in System Variables to pass things like version numbers or Environment names to Process Step.
- [Variable Sets] How to use Variable Sets to share common settings across multiple Projects.
- [Variable Replacement] How to replace generic, default values in configuration files during Deployments.

[![Link to YouTube video](https://img.youtube.com/vi/Hd71uhcD61E/0.jpg)](https://www.youtube.com/embed/Hd71uhcD61E)

### Transcript

Let's start by taking another look at the Hello World project we created earlier in this module.

[Fade to process page for Hello World Project]

The Process for this Project has a single Step that runs a PowerShell script to log a greeting. Let's imagine that we wanted to issue a different greeting in each environment. To do that, let's navigate to the Variables page.

[Click Variables]

This table stores the Project Variables for our Deployment Process. We'll start by creating a Variable called FundamentalsDemos.HelloWorld.Greeting.

[Add variable called FundamentalsDemos.HelloWorld.Greeting]

We'll add a value,

[Add value: Hello, Development!]

and while we're here, let's make a note that we can select a specific Variable Type. For example, if this value was a password, I might choose to set the variable to Sensitive. This will ensure the value is encrypted in the Octopus database and that it is never revealed in any Deployment Logs.

[Set the value to sensitive, then undo it]

We can also open a larger editor for more complicated Variables. As well as a larger text editor, this includes additional options such as adding descriptions for our variables or enabling users to prompt for variables when triggering deployments.

[Open editor, click DONE]

Since we only want to use this value in Development, we'll scope this value to the Development Environment.

[Scope to Development]

While we're at it, let's add another value for Production.

[Add another value for Production, pause while scoping]

In this case, we are scoping our variable based on the Environment we are deployling to. However, it's also possible to scope in other ways. For example, we could instead scope variables to specific Deployment Targets or Target Roles.

[Finish adding the variable, click SAVE]

All done. Now we need to reference our variable from the script in our process.

[Click Process, open the Step, navigate to the script block]

Next to the script block, we can see the Variable Insert Tool on the right-hand side. Depending on the scripting language we are using, the syntax for referencing Octopus variables will be a little different. Clicking the Variable Insert Tool will display our Project Variables, along with other Octopus System Variables. We'll talk more about System Variables later, but right now we'll select the Variable we just configured and Octopus will add it to the script block using the necessary syntax. For more information about the various syntax for referencing variables in your given context, check out the additional resources associated with this module.

Let's just tidy up the script and click save.

[Tidy up script, click SAVE]

Now when we execute a Deployment, the appropriate value will be used when we deploy to each Environment.


Tips:

- Namesspace
- Use groups
- Keep var numbers low
https://octopus.com/docs/projects/variables