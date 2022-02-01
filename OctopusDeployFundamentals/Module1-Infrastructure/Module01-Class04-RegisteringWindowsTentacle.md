# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 4: Registering a Windows Tentacle Deployment Target

NOTE: The existing fundamentals video below is there as a placeholder. It includes a bunch of the content we can use, but isn't an exact match for what I want to do with this video. We should rerecord this video before publishing.

Welcome to class 4 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

[![Link to YouTube video](https://img.youtube.com/vi/CBws8yDaN4w/0.jpg)](https://www.youtube.com/embed/CBws8yDaN4w)

### Transcript

In this class we'll:

- Register a Windows Tentacle against our Octopus Deploy Server,
- Add our Tentacle to an Environment, and
- Assign our Tentacle a specific Target Role.

For the Octopus Server we'll use a free Octopus Cloud trial. For the Deployment Target, we'll use a Windows instance running in AWS EC2. If you would like to learn how to set up other types of Deployment Targets, such as a Linux or MacOS server, a Cloud Region, a Kubernetes Cluster or an Offline Package Drop, check out the additional resources associated with this module.

Here is the AWS instance we used from class 3, complete with an Octopus Tentacle that we've already installed and configured.

In our example, we want to use this instance to host the development version of a dotnet core web app. IIS and dotnet core have already been configured on the Target instance. If we open the Tentacle Manager we can see that it's healthy. Now we need to register our Tentacle with the Octopus Server to enable the two-way communication between the Server and Tentacle.

We're going to start by navigating to the Infrastructure page in the Octopus Cloud web portal. As you can see, we've already created a couple of Environemnts called Development and Production. We haven't yet registered any Deployment Targets or assigned any Target Roles.

We manage our Deployment Targets on the Octopus Server by clicking Deployment Targets. On this page we can add new Deployment Targets, disable or delete Targets, check the status of a Target, and run Health Checks.

To register our Deployment Target, click ADD DEPLOYMENT TARGET.

We're presented with various different options. We'll chose a Windows instance in listening mode.

Select Windows, then hover over Listening Tentacle and click ADD. This brings us to the registration page. Enter the DNS name or IP address of the Deployment Target, as well as the port which we configured it to listen on. (10933 by default.) We aren't connecting through a Proxy so accept the defaults and click NEXT.

We want to give our Target a descriptive name so it's easily identifiable in task logs or when managing our infrastructure. Machine names work well, but you might prefer to name it after the service or application that you intend to deploy to it. For example, helloworld-webserver001 or CRM-Database01.

At Octopus we subscribe to the philosophy of treating servers like cattle, rather than pets. For more information about the Cattle and Pets metaphor, check out the additional resources associated with this module. The point is that it's generally wiser to think of Deployment Target names like numbers or IDs, rather than using cute Lord of the Rings or Star Wars themed naming conventions. In this case, we'll use the randomly assigned AWS instance ID, since this helps us to keep track of things across both Octopus and AWS.

Next we assign one or more Environments and Roles. We're going to use this Target to host the Development version of the RandomQuotes dotnet Core App from [the Octopus Samples GitHub repo](https://github.com/OctopusSamples/RandomQuotes). Hence, we'll assign this Target to the Development Environment and we'll give it the role RandomQuotes-WebServer. In this example, we aren't using a Web Proxy so we'll leave those settings alone and click SAVE, which brings us to the settings tab for our new Target.

If we click Connectivity, we can verify that the Server and Tentacle can communicate successfully. We don't yet have any Deployments or Events to review, but later we can return here to review a full audit of all the tasks executed by our Deployment Target.

If we return to our Infrastructure page we now see that our Development Environment contains one Deployment Target. That Target has been assigned the Role RandomQuotes-WebServer. If we wanted, we could repeat this process using another Windows instance to set up another Deployment Target for Production.

In our example, since both the Server and Tentacle are hosted for us, our networking issues have been relatively simple. As long as we remember to open port 10933 on the Target instance, we should be OK. However, networking can be a tricky beast. If you have any problems repeating these steps for yourself, check out the additional resources for troubleshooting advice.

While this process was relatively straight-forward, it was manual and time consuming. For larger estates, or for folks who embrace dynamic infrastructure or chaos engineering, it will be important to investigate automated methods for registering Deployment Targets. Check out the additional resources to learn how to repeat these steps using the Octopus API or command line interface.

Now it's your turn to register your Deployment Targets. Remember:

- Think about the DevOps "Cattle vs Pets" mantra when choosing names for your Deployment Targets. Aim to give your servers systematic numbers or IDs, rather than cute names.
- Folks with large estates or who wish to use dynamic infrastructure or embrace Chaos Engineering should learn more about automating Deployment Target registration using the Octopus API and command line tools.
- Troubleshooting information is available in the additional resources that accompany this module.

Thank you for watching, and happy deployments.
