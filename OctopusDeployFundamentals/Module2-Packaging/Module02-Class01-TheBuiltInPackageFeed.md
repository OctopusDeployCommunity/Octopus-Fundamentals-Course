# Octopus Deploy: Fundamentals
## Module 2: Packaging
### Class 1: The Buit-In Package Feed

Welcome to module 2, class 1 of this Octopus Deploy Fundamentals cource. In this class, you'll learn how to package and present your code so that Octopus Deploy can deploy it to your infrastructure.

[![Link to YouTube video](https://img.youtube.com/vi/YOUTUBE-ID-GOES-HERE/0.jpg)](https://www.youtube.com/embed/YOUTUBE-ID-GOES-HERE)

### Transcript

We'll cover:

- Why Octopus needs packages, and the formats Octopus supports
- Your options for hosting packages
- How to upload a package to the built-in package feed

To deploy with Octopus, you first need to package any deployment artifacts required for deployment into a format that Octopus can consume. Most often this means zipping up all the necessary files. However, depending on what you are building, you might prefer to use a different file format, such as NuGet, JAR or Tar, or even Docker images. A full list of supported formats can be found in the additional resources associated with this module.

Once Octopus has the packages, it can copy them to Deployment Targets, and run any scripts required to set things up.

Octopus comes with a built-in package repository. You can navigate to the built-in repository in the Octopus Deploy web portal by navigating to Library, and then Packages. For most users, the easiest way to get started is to upload their files directly in the browser. You can do this by clicking UPLOAD PACKAGE and drag/dropping your packages like this.

I created this package by cloning the RandomQuotes GitHub repository from Octopus Samples, building the solution, and zipping up the build output. However, Octopus provides various tools for automating this process. For more information about packaging your code, take a look at the additional resources associated with this module.

Note that we've used a specific naming convention so that Octopus can interpret the version number of our code. We recommend adopting a consistent versioning convention, such as major version dot minor version dot build number.

While uploading packages manually is handy for a quick proof of concept, for most real-world implementations of Octopus Deploy, it's recommended to automate the packaging and publishing process. Most users automate this using build servers, such as TeamCity, Jenkins, Azure DevOps or GitHub Actions. Code updates are automatically compiled and tested. Then, assuming all the tests pass, the build artifacts are automatically packaged and published to Octopus for deployment.

Octopus provides a number of tools to help with automated packaging and publishing. For more information about these, check out the additional resources associated with this module.

While the built-in package feed meets the needs of most users, Octopus also supports various types of external feeds. For example, if users already use some other package feed, or if they prefer to set up a separate package manager, they can integrate their own package feed with Octopus Deploy. For more information about external package feeds, check out the additional resources associated with this module.

Remember:

- If you don't already have one, start with the built-in package repository
- Adopt a consistent semantic versioning strategy to help you keep track of the different versions of your code
- Automate packaging and publishing process using a build server

Thanks for watching, and happy deployments.