# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)

### Class 4: Variables

Welcome to module 3, class 4 of this Octopus Deploy Fundamentals training course. This class is about Variables.

So far in this module we've already set up a couple of Projects and we've successfully deployed a sample website. Along the way, we explained that Octopus believes in using consistent deployment processes to each Environment. It's simpler and safer to re-use the same Packages and Processes for Deployments to development and production.

However, often there are important differences that need to be accounted for. For example, perhaps we need to use different database connection strings in different Environments. Or perhaps we need to provide some sensitive information, such as a password, that we don't want to keep in source control.

Variables solve this problem by enabling us to pass either plaintext or encrypted values to our Deployment Processes.

In this class, we'll talk about:

- [Scoping] Scoping variables so that we can feed different values in different contexts.
- [System Variables] Using the built in System Variables to pass things like version numbers or Environment names to Process Step.
- [Variable Replacement] How to replace generic, default values in Structured Configuration Files during Deployments.
- [Library Variable Sets] How to use Library Variable Sets to share common settings across multiple Projects.

[![Link to YouTube video](https://img.youtube.com/vi/Hd71uhcD61E/0.jpg)](https://www.youtube.com/embed/Hd71uhcD61E)

### Transcript

Let's start by taking another look at the Hello World project we created earlier in this module.

[Fade to process page for Hello World Project]

The Process for this Project has a single Step that runs a PowerShell script to log a greeting. Let's imagine that we wanted to log a different greeting in each environment. To do that, let's navigate to the Variables page.

[Click Variables]

This table stores the Project Variables for our Deployment Process. We'll start by creating a Variable called FundamentalsDemos.HelloWorld.Greeting.

[Add variable called FundamentalsDemos.HelloWorld.Greeting]

We'll add a value...

[Add value: Hello, Development!]

... and while we're here, let's make a note that we can select a specific Variable Type. For example, if this value was a password, I might choose to set the variable to Sensitive. This will ensure the value is encrypted in the Octopus database and that it is never revealed in any Deployment Logs.

[Set the value to sensitive, then undo it]

We can also open a larger editor for more complicated Variables. As well as a larger text editor, this includes additional options such as adding descriptions for our variables or enabling users to provide their own values when triggering deployments.

[Open editor, click DONE]

Since we only want to use this value in Development, we'll scope this value to the Development Environment.

[Scope to Development]

While we're at it, let's add another value for Production.

[Add another value for Production, pause while scoping]

In this case, we are scoping our variable based on the Environment we are deployling to. However, it's also possible to scope in other ways. For example, we could scope to specific Deployment Targets or Target Roles.

[Finish adding the variable, click SAVE]

All done. Now we need to reference our Variable from the script in our Process Step.

[Click Process, open the Step, navigate to the script block]

Next to the script block, we can see the Variable Insert Tool.

Clicking the Variable Insert Tool will display our Project Variables, along with other Octopus System Variables. We'll talk more about System Variables later.

Selecting our variable adds it to the script with the appropriate syntax. For more information about syntax in various languages, check out the additional resources associated with this module.

Let's tidy up the script and click save.

[Tidy up script, click SAVE]

Now when we execute a Deployment, the appropriate greeting will be used in each Environment.

[Fade to brief demos of deployments to Dev and Prod, reviewing the logs for the message in each environment]

This is all well and good for a simple, Hello World, example, but how would we use Variables when deploying a real website?

[Fade to RandomQuotes website, as deployed without any Structured Configuration Variables]

Here's the website we deployed in the last class. If we take a look at the footer, it's displaying the environment name and the version number. However, this version number is incorrect and the Environment name (Dev) doesn't match our configuration in Octopus Deploy (where we used the unabreviated "Development").

[Fade to this GitHub page: https://github.com/OctopusSamples/RandomQuotes/blob/master/RandomQuotes/appsettings.json]

That's because the website is still using default values defined here, in source control. We need to replace these default values with Octopus Variables when we execute Deployments.

[Fade to Process for RandomQuotes Project]

Here's the Process we set up in the previous class to deploy the RandomQuotes website. 

[Scroll down, highlight the Structured Configuration Variables section]

When we configured this project, we skipped over the Structured Configuration Variables options.

Let's update the Project to reference the file that contains our configuration variables. Octopus can update values in JSON, YAML, XML and Java Properties files.

Octopus expects the relative path to the configurtation file from the route of the Package. Since our configuration file is in the route of our package, we only need the file name.

[Type appsettings.json, and save.]

Now let's hop over to the Variables page to enter our values.

[Click Variables]

We can use this syntax to reference the variables in our configuration file.

[Add AppSettings:EnvironmentName]

As for the value, we could hard code it like we did before, entering in different values and scoping them to different Environments. However, in retrospect this feels a bit cumbersome. Perhaps in the future we'll rename an Environment or add a new one? It would be better to use the built-in Octopus System Variable, Octopus.Environment.Name, to automatically populate this value for us.

[Add value #{Octopus.Environment.Name}]

For the version number, we can use another System Variable to reference the Release number.

[Add a new variable: AppSettings:AppVersion and add value #{Octopus.Release.Number}]

Links to the documentation for System Variables, as well as all the relevant variable syntax we've used, can be found in the additional resources.

Now, let's redeploy the website. Remember, since we've changed our Process and our Variables, it's necessary to create a new Release. If we were to re-deploy the old Release, we'd be redeploying the old Process and Variables which would not reflect the changes we've just made.

[Create release, redeploy to development, refresh website, highlight the new environment name and version number]

Finally, there are times when we might want to share variables across multiple Projects. For example, perhaps we have some standard conventions for logging and we want to apply them globally.

Rather than duplicating our configuration across many Projects, we can head to the Library page and create a Variable Set.

[Go to Library, Variable Sets, click ADD NEW VARIABLE SET]

We can give the Library set a name and a description.

[Name: Logging. Description: Default config for logging.]

Let's add a couple of variables to our set.

[Create variables:
- Logging.Level: Info
- Logging.Location: \\logs\#{Octopus.Environment.Name}\#{Octopus.Project.Name}
SAVE
]

Note that you can reference either System Variables, or your own Variables, within other variables. In this case to ensure that the logs for different Projects and Environments are saved in different locations.

Let's go back to our Project to include this Variable Set.

[Click Projects / RandomQuotes / Variables / Library Sets / INCLUDE LIBRARY SET / Select Logging / Click SAVE / Expand the Logging Variable Set to reveal values]

Great, now this Project can access Variables that have been set at a global level.

We've covered a lot of details in this class, so let's recap:

Variables are used to provide flexibility and privacy with important deployment details.

- [Project Variables] Typically we use Project Variables to provide sensitive details, or details that change depending on the context.
- [Types, Scoping, Sensitivity, and Prompting] Octopus supports various features to support different Variable Types, Scopes, Encryption, and the ability to set values when triggering Deployments.
- [System variables] As well as setting your own variables, you can, and should, make use of the many built-in System Variables.
- [Variables within variables] You can reference Variables within other Variables.
- [Structured Configuration Variables] As well as referencing Variables within your scripts, you can also import them into configuration files. 
- [Library Variable Sets] You can use Library Variable Sets to manage global Variables in a single location, avoiding the need to duplicate common configuration details across multiple Projects.

Let's finish with a few tips to remember when creating your own variables.

- [Use descriptive variable names] Use descriptive variable names, not only for your convenience, but also for the sake of others who may need to understand how and why your variables are used.
- [Namespace your variables] Always namesspace your variables. The variable "password" is fairly generic, while the variable SQLServer.Admin.Password provides much more context. Also, it's a good idea to try and avoid re-using the same variable names across multiple Projects and Library Sets. By including the Project or Variable Set name, we reduce the risk of confusion or bugs caused by using the same Variable name in multiple places. 
- [Use Variable Sets] Remember to use Variable Sets for any values that are likely to be useful globally. Over time this can significantly reduce duplication and administrative toil.
- [Keep Variable Numbers Low] And finally, while Variables are critical for using Octopus effectively, it's possible to overuse them. If you have many configuration settings for your application and are using an Octopus Variable for each value, it's possible that Octopus may not be the best place for those values. Consider whether those settings are mostly static or whether it's safe to store them in clear text. If so, it might be worth considering using an external store, source control repository, configuration management system or a database to hold this information. Generally, for Deployment purposes, it's best to use Octopus Variables primarily to hold information associated with deploying software, rather than configuring it.

Thanks for watching, and happy deployments!