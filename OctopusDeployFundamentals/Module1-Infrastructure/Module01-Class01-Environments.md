# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 1: Environments

Welcome to another getting started class for Octopus Deploy. This class will help you learn more about environments.

<iframe width="560" height="315" src="https://www.youtube.com/embed/tPb6CLHyNLA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Transcript

Environments are how you organise your deployment targets into groups that represent different stages of your deployment pipeline. This class will start with a look at a pre-existing instance, to see how environments are used. It will then walk you through how to create your first environment.

We will start using an existing instance. You get to environments by clicking on "Infrastructure", then clicking on Environments in the left menu. For this existing instance I have six environments:

I stated earlier Environments are used to organise your deployment targets. The development environment has three targets, while the test environment has eleven targets.

Now let's create your first environment. To make things easier, the onboarding wizard provides a shortcut to the environments page. 

From here we can click the "ADD ENVIRONMENT" button in the top right corner.

This will bring up the "Add Environment" modal window. To make it easier, we've provided a list of common environment names. Clicking on the name, will populate the text box. 

Once you are done, click "SAVE" and the environment will be created.

You have just created your first environment. If you'd like, you can add a description to help other users understand the purpose of this environment. This is useful if the environment's name isn't clear to everyone, or if it has an unusual purpose.

That description will appear in the environment list page. Expanding the environment, will show the description previously entered.

Now it is your turn to create your first environment. Here are some recommendations to keep in mind as you do that in your own instance.

- Reuse the same environments across multiple projects. Don't create a unique set of environments per project.
- Use names common to your company, such as Dev or Development, Test or QA, Staging or Pre-Prod, as well as Production.
- Only abbreviate common terms known across the industry, such as QA, instead of Quality Assurance. This will help prevent confusion in the future.
