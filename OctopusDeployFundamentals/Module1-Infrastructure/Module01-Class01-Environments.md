# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 1: Environments

Welcome to class 1 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

This class covers how to manage Environments in Octopus Deploy.

[![Link to YouTube video](https://img.youtube.com/vi/tPb6CLHyNLA/0.jpg)](https://www.youtube.com/embed/tPb6CLHyNLA)

### Transcript

Environments are how you organise your infrastructure into groups that represent different stages of your deployment pipeline. For example, you might have a Development environment, and a Production environment.

Let's create your first environment.

In this example, we're using a new Cloud instance of Octopus Deploy. To make things easier, the onboarding wizard provides a shortcut to the environments page. 

From here we can click the "ADD ENVIRONMENT" button in the top right corner.

This will bring up the "Add Environment" modal window. To make it easier, we've provided a list of common environment names. Clicking on the name, will populate the text box. 

Once you are done, click "SAVE" and the environment will be created.

You have just created your first environment. We can repeat the process to create a second Environment.

You should order your environments in chronological order. To reorder your environments, click the three-dot menu button and select Reorder. Drag your environments into the desired order, and click save.

Now it is your turn to create your first environment. Here are some recommendations to keep in mind as you do that in your own instance.

- Reuse the same environments across multiple projects. Don't create a unique set of environments per project.
- Use names common to your company, such as Dev or Development, Test or QA, Staging or Pre-Prod, as well as Production.
- Only abbreviate common terms known across the industry, such as QA, instead of Quality Assurance. This will help prevent confusion in the future.
