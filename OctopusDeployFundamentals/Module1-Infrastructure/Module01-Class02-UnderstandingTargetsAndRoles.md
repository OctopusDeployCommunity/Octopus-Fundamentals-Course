# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 2: Understanding Deployment Targets and Machine Roles

Welcome to class 2 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

EMBED VIDEO
DRAFT VERSION ONLY: https://drive.google.com/file/d/1GqJ9LEaTpFzPFrz39uxbgJodcXxAq0Jl/view?usp=sharing

### Transcript

This video will explain the purpose of "Deployment Targets" and "Machine Roles", as well as the relationship between them. Understanding how Targets and Roles work will be an important foundation ahead of the next class where we'll begin to configure our infrastructure.

We'll cover:

- Definitions for both Deployment Target and Machine Roles. 
- How to use Machine Roles to configure which tasks get executed on each Deployment Target within each environment. 
- And advice on Machine Role and Deployment Target naming conventions.

Deployment Targets are the machines and services where your application gets deployed. For example, this might be a physical or virtual machine running in AWS, Azure, GCP, or your own data centre. Octopus also has native support for various Platform-As-A-Service endpoints, such as Azure Web Apps or AWS ECS Clusters. You can also set up either a Kubernetes Cluster or a specific Cloud Region as a Deployment Target. Finally, where direct connections are impossible, Octopus supports offline package drops, enabling targets to pull the latest updates on their own schedule, without granting any access to Octopus Deploy.

In this case we have six VMs running in Amazon EC2. We are using Windows instances to host our dotnet core web apps and Linux instances to host SQL Server and our load balancer. Typically, for simplicity, in Octopus we'll name our Targets after their respective machine names.

As discussed in the previous class, targets are organised into one or more Environments, such as "Development" or "Production". 

We use Machine Roles to define what each Target within an Environment is responsible for. For example, in this case we have a SQL Server instance in each of our Dev and Test environments. We also have a few web servers, with the production web servers sitting behind a load balancer. We've assigned the various servers the appropriate Machine Roles so that Octopus knows which parts of the deployment need to be executed against each Target Machine, within each environment.

For example, in this scenario, if we were to deploy our website to the production Environment, Octopus would know that the website would need to be deployed to Targets Web02 and Web03, and any database updates would need to be executed on DB02.

Now let's consider a little more complexity: Imagine we wanted to use Octopus to manage the deployments for both our website and our documentation pages. These are managed as independent projects and need to be deployed to different target machines. 

This example demonstrates the value of defining a standard naming convention for Machine Roles that incorporates both the Project Name, as well as the type of server. For example, website-webserver or docs-database. Note that Deployment Targets can have multiple Machine Roles.

Furthermore, Octopus Deploy isn't only a deployment tool. Operations Runbooks allow us to run routine or emergency maintenance tasks, in a fully audited manner using version controlled scripts. For example, we might want to use an Operations Runbook to install the latest SQL Server updates or instruct our load balancer to remove a troublesome web server from rotation.

With this in mind, it can be useful to use additional generic roles to define which targets are used to host SQL Server instances, load balancers, IIS etc.

Let's see how our example looks in the Octopus Deploy UI.

If we navigate to the Infrastructure tab, we can see that our two Environments each contain some Targets. We can also see Target Role that we've assigned. If we select Deployment Targets, we can see that each target has been given at least one role, and has been added to at least one environment.

To recap, here are some key tips to remember as you create your own Deployment Targets and Machine Roles:

- Use machine names for Deployment Targets.
- Use a specific Machine Role naming convention on Deployment Targets, including the Deployment Project Name. For example: Website-WebServer or Docs-Database
- Use generic Machine Roles for maintenance runbooks. For Example: IIS or MSSQL

Thank you for watching, and happy deployments.

