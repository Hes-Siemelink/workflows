# Part 1 - Introduction

Digital.ai Release 23.3 contains an exciting new feature called Workflows.

In this video I will tell what workflows are about, how to run them and how to create custom workflows for your organization.

Workflows can be used by Platform and development teams to automate activities such as infrastructure launches, application deployments, and service management.

Workflows are interactive, providing a standardized service that allows for customization.

Based on the acclaimed Release execution engine, workflows integrate with popular technologies like AWS, Azure, Kubernetes and ServiceNow.

You can easily author a new workflow from within Digital.ai Release and publish it for all teams in your organization to use.

Workflows have an easy-to-use interface, providing only the necessary steps needed to execute complex scenarios involving multiple technologies.


# Part 2 - Run sample workflow

Let's take a look.

Digital.ai Release 23.3 features a new Home page, that highlights its most used features. It is completely customizable.

On the widget that say "Introducing Workflows", simply click Run Workflow.

This will take you to the Workflow catalog page, that displays all workflows that are installed in the system.

Out-of-the-box, Digital.ai Release 23.3 contains curated workflows that are published by Digital.ai. When authoring workflows that are specific for your organization, they will show up on this page as well. Note that with our rich permission system, Platform teams can choose which folders are permitted to contribute to the catalog, hiding work in progress until it is ready to be published.

On the Catalog page, we can simply select a workflow and run it. For example, let's take the workflow called "AWS Lambda application setup with Deploy"

This workflow will set up a project that does Amazon Lambda deployments through our Deploy product, and keeps track of the deployed versions in Digital.ai Release.

Workflows are typically used to combine multiple technologies together, abstracting away from the nitty gritty details. Workflows provide a simple and unified interface. This way, users setting up a new product don't need to wade through tutorials of the various system, but can make use of best practices out of the gate.

To launch a workflow, simply click Run Workflow, and select the folder where you want to run it.

This is the main UI of the workflows. It is a simple view that shows you the steps that need to be done, with explanations about what's going on and simple form elements to provide the necessary configuration.

Here we need to specify which Deploy server to connect to. I simply select a preconfigured server called Deploy and hit next. 

To set up Digital.ai Deploy correctly, we need specify the name of the new environment we are creating.

Now the environment is being created in the Deploy product through automation.

And so it continues... On the surface workflows are simple steps that either ask user input or perform some automation.

Let me skip towards the end.

This workflow has configured an AWS Lambda app in Digital.ai Deploy and has registered it in Digital.ai Release.

The workflow is completed and Release will now receive live updates of the application on the Application Management screen.

# Part 3 - Under the hood

Now let's take a look of what happens under the hood.

In Digital.ai Release 23.3, standard workflows are provided out-of-the-box in the "Digital.ai - Official" folder.
These are stored as YAML and synchronized with a public Git repository. 

Let's see what a workflow template looks like. We go into the Deploy folder, and select workflows.

Workflows are very similar to releases. We have workflow templates and workflow executions. Workflows use the same execution engine as releases. When authoring a workflow template, you will see the familiar release flow editor that contains all the steps of the workflow as tasks. This is the template of the workflow we just ran, and you will see it contains the workflow steps as tasks.

There are some differences between workflows and releases.

Workflows are meant for shot-lived, single user automation flows. 

Therefore, they do not support team collaboration, scheduling and other advanced orchestration capabilities of Digital.ai Release.

All integration tasks are supported, and most of the core tasks.

# Part 4 - Create a new workflow

Let's create a new workflow.

We will start author the new workflow outside the "Digital.ai Official" folder, that is read-only.

We will create a Workflow to set up a new GitHub repository based on a template repo and with some customization.

I created a new folder "Team Workflows". Now I go into Workflows and create a new template.

Let's create a workflow template called "Create new repo"

First we will add the steps we need to do as manual steps.

There are two steps

1. Create repo from template
2. Customize project

We will simply add these as manual tasks and provide some instructions.

For example, go to the template project, and create a new repo that follows our naming conventions
And then: Change the README to say which team owns it.

As a best practice, save the project in Git using folder versioning. Let me load a pre-built example. 

We can already run it! It doesn't do very much yet, but we have a simple skeleton that we can build upon.


# Part 5 - Adding a form

Now we will add some input fields on a form. We do this by using variables.

The simplest way to add a variable is to just go into a description and add a variable name in dollar-curly syntax. 
The variables will be created automatically.

We can now add a User Input task that will display the form.

Edit the description and add the variables that you just created.

Let's run the new version.

It will display a new first step, and the values that we fill in here are picked up on the subsequent screen.

We can tweak how the form fields are displayed in the Variables section.

Let's go back to the workflow template and select "Variables"

We can give the variables a display name and description.

When creating a new variables, you can select from various form elements like boolean checkboxews, dropdowns, etc. to build the form.

Here's a version that I have prepared before. Let's run it.

You will see that we have a nice form.

The values that you entered are used in the subsequent steps.

# Part 6 - Automation

But still, it is a manual process.

It's time to automate some steps.

Let's go back to the template and change the manual steps to automated ones.

For this demo, I have created some integration tasks with GitHub using the new SDK 2.0. 

I am changing the task type to GitHub, Create new repository from template.

Now let's fill in the blanks.

Also the next task. We will use the 'Modify file' task here to update the README.

We need the location of the repository that is just created. It's the output of the previous task. Let's go there and introduce a new variable, "repo". This points to the repository that is just created.

And we can use it in the next task.

You can use also variable references to populate the README.

Finally we will add a closing task informing the user of the location of the new repository. We can create a hyperlink in Markdown syntax. 

Now let's run this final version.

In the end the new repository is created and ready to use!

# Part 7 - Conclusion

This concludes the demo.

Summarizing: we have created a workflow that asks the user for the essential information.

Then all the necessary work is automated behind the scenes. We used the visual authoring environment to integrate with GitHub and present the result ot the user.

In a real world scenario I would go on to set up permissions, CI, test environments, wire up a release template, etc. Unifying all these different steps underthe umbrella of a Workflow, with a simple user interface.

Workflows are in available in the Early Access releases of Release 23.3. Please take it for a spin!

