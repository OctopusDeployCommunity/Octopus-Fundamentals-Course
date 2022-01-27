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

We haven't yet registered any Deployment Targets or assigned any Target Roles. We explained the conepts of Deployment Targets and Target Roles in class 2.

If we RDP into our Windows EC2 instance, we can open the Tentacle Manager. This is the same Tentacle we set up in class 3.

Our objective is to set up the communication between our Octopus Server and our Windows Tentacle so that we can use Octopus Deploy to run Tasks, such as Deployments or Operations Runbooks, on our EC2 instance.

We manage our Deployment Targets by clicking Deployment Targets. On this page we can add new Deployment Targets, disable or delete Targets, check the status of a Target, and run Health Checks.

To register our Deployment Target, click ADD DEPLOYMENT TARGET.

We are presented with various different options. For example, Octopus Deploy supports multiple methods for connecting to Windows, Linux or Mac machines, as well as other options for Kubernetes, cloud providers or even "offline" use cases where it's impossible to connect directly to the intended targets.

We're connecting to a Windows instance in listening mode. We discussed the difference between Listening and Polling Tentacles in Class 3. Check out the additional resources for this module for tutorials to configure other types of Deployment Targets.

Select Windows, then hover over Listening Tentacle and click ADD. This brings us to the registration page. Enter the DNS name or IP address of our Deployment Target, as well as the port which we configured it to listen on. (10933 by default.) We aren't connecting through a Proxy so accept the defaults and click NEXT.

We want to give our Target a descriptive name so it's easy to identify in task logs or when managing our infrastructure. Machine names work well, but you might prefer to name it after the service or application that you intend to deploy to it.

(2:20)
