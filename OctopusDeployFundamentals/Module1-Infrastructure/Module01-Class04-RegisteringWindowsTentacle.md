# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 4: Registering a Windows Tentacle Deployment Target

NOTE: The existing fundamentals video below is there as a placeholder. It includes a bunch of the content we can use, but isn't an exact match for what I want to do with this video. We should rerecord this video before publishing.

Welcome to class 4 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

[![Link to YouTube video](https://img.youtube.com/vi/CBws8yDaN4w/0.jpg)](https://www.youtube.com/embed/CBws8yDaN4w)

### Transcript

In this class we'll:

- Register a Windows Tentacle against our Octopus Deploy Server
- Add our Tentacle to an Environment
- Assign our Tentacle a specific Target Role

For the Octopus Server we'll use a free Octopus Cloud trial. For the Deployment Target, we'll use a Windows instance running in AWS EC2. If you would like to learn how to set up other types of Deployment Targets, such as Linux or Mac servers, cloud regions, kubernetes clusters or offline package drops, check out the additional resources associated with this module.

In our example, we want to use this instance to host the development version of a dotnet core web app. IIS and dotnet core have already been configured on the Target instance. We installed and configured our tentacle in class 3. If we RDP into our EC2 instance, we can open the Tentacle Manager and we can see that it's healthy. Now we need to register our Tentacle with the Octopus Server to enable the two-way communication between the Server and Tentacle.

We're going to start by navigating to the Infrastructure page in the Octopus Cloud web portal. As you can see, we've already created a couple of Environemnts called Development and Production. We covered Environment creation in Class 1 so we won't repeat ourselves here.

We haven't yet registered any Deployment Targets or assigned any Target Roles. We explained the conepts of Deployment Targets and Target Roles in class 2.

We manage our Deployment Targets on the Octopus Server by clicking Deployment Targets. On this page we can add new Deployment Targets, disable or delete Targets, check the status of a Target, and run Health Checks.

To register our Deployment Target, click ADD DEPLOYMENT TARGET.

We are presented with various different options and we'll chose a Windows instance in listening mode. We discussed the difference between Listening and Polling Tentacles in Class 3.

Select Windows, then hover over Listening Tentacle and click ADD. This brings us to the registration page. Enter the DNS name or IP address of our Deployment Target, as well as the port which we configured it to listen on. (10933 by default.) We aren't connecting through a Proxy so accept the defaults and click NEXT.

We want to give our Target a descriptive name so it's easy to identify in task logs or when managing our infrastructure. Machine names work well, but you might prefer to name it after the service or application that you intend to deploy to it. We're going to use the AWS instance ID.

Next we assign one or more Environments and Roles. The concepts of Environments and Roles were covered in classes 1 and 2. We're going to use this Target to host the Development version of the RandomQuotes dotnet Core App from [the Octopus Samples GitHub repo](https://github.com/OctopusSamples/RandomQuotes). Hence, we'll assign this Target to the Development Environment and we'll give it the role RandomQuotes-WebServer. In this example, we aren't using a Web Proxy so we'll leave those settings alone and click SAVE.

Additional resources:
- Network troubleshooting
- Security deep dive (Should this be a class in it's own right?)
- Other deployment types

