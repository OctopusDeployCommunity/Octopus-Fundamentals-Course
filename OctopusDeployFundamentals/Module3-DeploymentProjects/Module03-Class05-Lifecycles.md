# Octopus Deploy: Fundamentals
## Module 3: Projects (Part 1, Deployments)
### Class 5: Lifecycles and Channels

Welcome to module 3, class 5 of this Octopus Deploy Fundamentals training course. In this class we'll cover Lifecycles and Channels. Lifecycles enable us to define what order our Environments should be deployed to. Channels allow us to change various settings for different sorts of Releases. For example, perhaps you want to handle Releases from your main branch differently from feature branches.

[![Link to YouTube video](https://img.youtube.com/vi/ofc-u61ukRA/0.jpg)](https://www.youtube.com/embed/ofc-u61ukRA)

[Slides]

So far, we've only been using two Environments: Development and Production. We specified that Development should come first. By default, Octopus enforces that all Releases must work through the Environments in order. This made sense, up until now.

Now let's imagine we want to add a third Environment for the RandomQuotes website for User Acceptance Testing (UAT for short).

This Environment is for end users to try out significant new features before they go to Production. However, we wouldn't expect to use this Environment for smaller features or bug fixes.

[Fade to Environments page, with new UAT Environment]

We've repeated the steps we followed in Module 1 to build our new Environment, and we've adjusted the order such that UAT sits between Development and Production. However, we want deployment to UAT to be optional.

If we navigate to the Process page for the RandomQuotes Project...

[Navigate to RandomQuotes Process page]

... we can see that this Process uses the "Default Lifecycle", which enforces that Releases must be deployed to Environments in order. Let's create a new Lifecycle, with an optional UAT phase.

Lifecycles are managed under Library / Lifecycles.

[Navigate to Lifecycles page]

We'll add a new Lifecycle, called "UAT Optional".

[Click ADD LIFECYCLE, provide name and description]

First we are asked how long to retain Releases. We're happy with the default retention settings so we'll move on to edit the "Phases".

[Scroll down to phases]

A Phase is a step in your development lifecycle that can contain one or more Environments. In our case, we want a Phase for each Environment, but we want to make the UAT Phase optional.

[Add three Phases, setting UAT to optional]

At the bottom of the page, we can see our Lifecycle preview. This is a handy diagram for understanding Lifecycles at a glance.

Let's save our new Lifecycle, and apply it to the Deployment Process for our RandomQuotes Project.

[Navigate back to the Project page for RandomQuotes]

This Project currently uses the Default Lifecycle. We can change this by clicking "Change".

[Click Change, switch to "UAT Optional", click SAVE]

We can see that the Lifecycle for this project has been updated. Now the team can choose whether or not releases need to be deployed to UAT before Production on a case by case basis.

[Fade to slides]

The team has been using the new Lifecycle for a while and it's been working fine, up until now. 

Our users want the ability to add filters to the random quote generator, allowing them to pick quotes on certain topics or from different people. The development team has split into two sub-teams, a "filters" sub-team who will work closely with some BETA testers on the new feature, and a "core" sub-team, who will work on other features and general bug-fixes.

In order to support this, our sub-teams have agreed on a branching strategy. All work associated with the "filters" feature will live on a 'filters' branch, and all other work will live on the 'main' branch.

Further, the "core" sub-team have decided to embrace Continuous Deployment to the Development Environment. They want all updates to the 'main' branch to be automatically deployed to Development. This will provide rapid feedback if any code updates result in a deployment failure and ensures that the Development Environment will never be more than a couple of minutes behind the latest version from source control.

To achieve this, the team has made a few changes, both in Octopus Deploy, and also in their build process.

[Fade to Packages page, displaying a list of RandomQuotes packages at different versions, including pre-release tags]

The team uses a build server to automatically build their packages and upload them to the Octopus built-in Package feed. If we look at the existing packages we can see that the versions' for some of the newer packages have a "filters" pre-release tag. That's because the build process has been configured to automatically suffix the branch name to the version number, whenever it's building from a non-default source control branch.

The build process has also been configured to automatically create a new Octopus Release each time a new Package is uploaded. 

[Open the Releases page for the RandomQuotes Project in another tab, side by side with the Packages. Observe that all the numbers match.]

For more information about automatic Release creation, check out the additional resources associated with this module.

[Navigate to Lifecycles]

Our two sub-teams have started to use different Lifecycles. The "core" team still uses the "UAT Optional" Lifecycle. However, in order to support Continuous Deployment, it's now set to automatically deploy all new Releases to Development as soon as the Release is created.

The "Pre-Release" Lifecycle is used for any Releases with a pre-release tag. Effectively, this catches all builds from non-default source control branches. The "Pre-Release" Lifecycle can only be used to deploy to UAT. Since the "filters" team want to be deliberate about which versions they show the BETA testers, and they don't want new versions to be deployed during testing sessions, they didn't configure UAT for automatic deployment.

When the "filters" team is ready to deploy their work to Production, they merge their feature branch into the "main" source control branch. Following a fresh build, a new Release is created, this time using the "UAT Optional" Lifecycle. The Release will be deployed to Development automatically and, later, may be deployed to Production at will.

The team manage which Lifecycle each Release should use with Channels.

[Navigate to RandomQuotes / Channels]

We can see here that the Default Channel uses the "UAT Optional" Lifecycle. This is the lifecycle that we expect all packages without a pre-release tag to use. However, there's also a "Pre-Release" Channel, which uses the "Pre-Release" Lifecycle.

[Click on Pre-Release Channel]

The "Pre-Release" Channel uses a Version Rule for any Releases that contain a Package for RandomQuotes website with a version number that has a Pre-Release tag. The intention is to catch any updates to non-default source control branches. For now, that's just the "filters" branch, but in the future the team may use branches for other purposes.

[Click on "Version Rule 1"]

You can use either Mavern or NuGet syntax for these rules. There are some examples in the documentation ...

[Click documentation and scroll to examples]

... but since the syntax can be a little confusing, Octopus provides a handy "Design Rule" wizard to check your version patterns.

[Go back to Octopus, Open the Design Rule tool]

You can check your syntax against various test cases, to ensure that you've configured it correctly.

[Type in a few more examples and change the rule. Once done, cancel out of it.]

Let's take a look at how the team have been getting on.

[Navigate to the Project Overview page]

From the Project Overview page, we can see that the Releases have been filtered into different Channels. We can see that the recent releases on the Default Channel have mostly been deployed to Development and Production. We could deploy these to UAT if we wanted, but we don't have to deploy to UAT before deploying to Production if we don't want to. We can also see that all the Releases from the Default Channel have been deployed to Development since this happens automatically.

For the Pre-Release Channel, it's not possible to deploy to either Development or Production. Any Release could be deployed to UAT, but since Releases aren't deployed continuously, not all the Releases have been deployed. The team, in collaboration with the BETA users, have been selective about which versions to deploy, and when to deploy them.

