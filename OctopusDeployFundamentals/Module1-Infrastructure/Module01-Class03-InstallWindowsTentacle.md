# Octopus Deploy: Fundamentals
## Module 1: Infrastructure
### Class 3: Creating a Windows Tentacle Deployment Target

--

Welcome to class 3 of this Infrastructure module for the Octopus Deploy Fundamentals training course.

NOTE: This video link needs updating
[![Link to YouTube video](https://img.youtube.com/vi/HLpCodiH3Bc/0.jpg)](https://www.youtube.com/embed/HLpCodiH3Bc)

### Transcript

In this class we'll install an Octopus "Tentacle" on a Windows instance. Tentacles run on Windows or Linux and are responsible for receiving instructions from an Octopus Server, executing deployments and sending any logs back to the server.

We will cover:

- Downloading the tentacle installer
- Installing the tentacle on Windows
- and the difference between listening and polling tentacles, and when you should use each

For this demo, we're using a Windows intance running in AWS EC2. However, the process is the same, regardless of where the Windows machine is hosted.

You can download the Tentacle installer from Ocotpus.com by navigating to the Downloads page under the resources menu. Find the tentacle in the list of tools and click on the download button.

If you use Chocolatey to manage your software installs, you can install the tentacle with the command provided.

Otherwise, you can use the direct download links below.

Once it's downloaded, run the installer to start the setup wizard. Accept the licence agreement and provide an install directory. Once the Tentacle is installed, the Tentacle Manager will open. Click "Get Started".

The first choice is whether to set up the tentacle in listening or polling mode. A listening tentacle will passively listen for tasks requested by the Octopus Server. This is the recommended communitation style if you can allow connections from the Octopus Server to the Tentacle. If the Octopus Server cannot send requests to the tentacle, for example due to a firewal policy or when the Tentacle machine lacks a static IP address or DNS name, you should consider using polling mode instead.

Next, select where the Tentacle will store logs and applicatons.

On the Listening Tentacle tab, you can choose which port the Tentacle will listen for commands on. You can use the Octopus default of 10933, or you can choose a different port. You also need to provide the Thumbprint from your Octopus Server. This ensures the Tentacle will only trust your Octopus Server.

You can find your Octopus Server Thumbprint by logging into your Octopus Web Portal and navigating to Configuration / Thumbprint.

The last step is to install. You can use the Show script link to view the commands that the Tentacle Manager will run. This is useful for automating the Tentacle setup in your infrastructure.

Click the INSTALL button when you are ready, and you'll see the output of the commands in the text area below the button.

Once the install is complete, you can click the finish button and start using your Tentacle.

Note that the Tentacle also has a Thumbprint that needs to be provided to your Octopus Server when the Tentacle is registered. We'll register the Tentacle in the next class.

Here are some tips for configuring a listening Tentacle.

- Choose a listening tentacle if your Octopus Server can send requests to the machine hosting the Tentacle.
- You can automate the tentacle installation using a package manager like chocolatey and the Tentacle Manager command line interface.
- You can manage software upgrades for your Tentacle in your Octopus web portal.

Thanks for watching, and happy deployments.