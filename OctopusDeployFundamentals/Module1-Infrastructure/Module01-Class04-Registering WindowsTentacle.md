# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 3: Creating a Windows Tentacle Deployment Target

NOTE: The existing fundamentals video below is there as a placeholder. It includes a bunch of the content we can use, but isn't an exact match for what I want to do with this video. We should rerecord this video before publishing.

Welcome to class 4 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

[![Link to YouTube video](https://img.youtube.com/vi/CBws8yDaN4w/0.jpg)](https://www.youtube.com/embed/CBws8yDaN4w)

### Transcript

In this class we'll:

- Register a Windows Tentacle against our Octopus Deploy Server.
- Add our Tentacle to an Environment
- Assign our Tentacle a specific Target Role

For this class I'm using a free Octopus Cloud trial for the Octopus Server and a Tentacle running on a Windows instance in Amazon EC2.

We're going to start by navigating to the Infrastructure page in the Octopus Cloud web portal. As you can see, we've already created a couple of Environemnts called Development and Production. We covered Environment creation in Class 1 so we won't repeat ourselves here.

We can also see that we haven't yet registered any Deployment Targets or assigned any Target Roles. We explained the conepts of Deployment Targets and Target Roles in class 2.

Finally, if we RDP into our Windows EC2 instance, we can open the Tentacle Manager. This is the same Tentacle we set up in class 3.

Our objective is to set up the communication between our Octopus Server and our Windows Tentacle so that we can use Octopus Deploy to run Tasks, such as Deployments or Operations Runbooks, on our EC2 instance.



