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

Next to the script block, we can see the Variable Insert Tool on the right-hand side.

Clicking the Variable Insert Tool will display our Project Variables, along with other Octopus System Variables. We'll talk more about System Variables later.

Selecting our variable adds it to the script, with the appropriate syntax. For more information about syntax in various languages, check out the additional resources associated with this module.

Let's tidy up the script and click save.

[Tidy up script, click SAVE]

Now when we execute a Deployment, the appropriate greeting will be used in each Environment.

[Fade to brief demos of deployments to Dev and Prod, reviewing the logs for the message in each environment]

This is all well and good for a Hello World example, but how might we use these variables with something a little more complicated, such as a website.

[Fade to RandomQuotes website, as deployed without any Structured Configuration Variables]

Here's the website we deployed in the last class. If we take a look at the footer, it's displaying the environment name and the version number. However, this version number is incorrect and the Environment name (Dev) doesn't match our configuration in Octopus Deploy (where we used the unabreviated "Development").

[Fade to this GitHub page: https://github.com/OctopusSamples/RandomQuotes/blob/master/RandomQuotes/appsettings.json]

That's because the website is still using default values defined in source control. We need to replace these default values with Octopus Variables when we execute deployments.

[Fade to Process for RandomQuotes Project]

Here's the Process we set up in the previous class to deploy the RandomQuotes website. When we configured this project, we skipped over the Structured Configuration Variables options.

[Scroll down, highlight the Structured Configuration Variables section]

Let's update the Project to reference the file that contains our configuration variables. Octopus supports JSON, YAML, XML and Java Properties files.

[Type appsettings.json, and save.]

Now let's hop over to the Variables page to enter our values.

[Click Variables]

We can use this syntax to reference the variables in our configuration file.

[Add AppSettings:EnvironmentName]

As for the value, we could hard code it like we did before. However, in retrospect this feels a bit cumbersome. Perhaps in the future we'll rename an Environment or add a new one? It would be better to use the built-in Octopus Variable, Octopus.Environment.Name, to automatically populate this value for us.

[Add value #{Octopus.Environment.Name}]

[Then, add a new variable: AppSettings:AppVersion]

Similarly, we can use an Octopus Variable to pass through the version number for either the Package or the Octopus Release.

[Add value #{Octopus.Release.Number}]

Links to references of useful system variables, as well as relevant variable syntax, can be found in the additional resources.

Now, let's redploy the website. Remember, since we've changed our Process and our Variables, it's necessary to create a new Release. If we were to re-deploy the old release, we'd be redeploying the old Process and Variables which would not reflect the changes we've just made.

[Create release, redeploy to dev, refresh wesite, highlight the new environment name and version number]

[To do: VARIABLE GROUPS]

Tips:

- Namesspace
- Use groups
- Keep var numbers low
https://octopus.com/docs/projects/variables