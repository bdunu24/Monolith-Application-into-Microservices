# Monolith-Application-into-Microservices

## Introduction

Hello, and welcome! 

In today’s project we’ll be deploying a monolithic node .js application to a Docker container. Then, we will be breaking the monolith application into microservices, with zero downtime. The node.js application will host a simple message board with threads and messages communicating between users.

### What is a Monolith? Why Migrate to Microservices?

A **monolith** is an application that’s a single unit of deployment, handling multiple kinds of business services. It is usually all tightly grouped together. Difficulties may potentially arise as an application’s code base grows––it becomes complicated to update and maintain, which makes a traditional monolithic architecture hard to scale.

On the other hand, **microservices** take each core of those business services, and deploy as its own separate unit, which preforms only a single function. They communicate with other services through a well-defined Application Programming Interface (API). Microservices can be written using different frameworks and programming languages, and you can deploy them independently, as a single service, or as a group of services.

![](monovsmini.jpeg)

Both the monolithic and miniservices applications are secured and maintained using containers. **Containers** provide a standard way to package your application's code, configurations, and dependencies into a single object. Containers share an operating system installed on the server and run as resource-isolated processes, ensuring quick, reliable, and consistent deployments, regardless of environment. 

***Why use containers?***

**Containers** are a powerful way for developers to package and deploy their applications. Some benefits of using them are:

- **Less overhead**
    >> Containers require less system resources than traditional or hardware virtual machine environments because they don’t include operating system images.

- **Increased portability**
    >> Applications running in containers can be deployed easily to multiple different operating systems and hardware platforms.

- **More consistent operation**
    >> DevOps teams know applications in containers will run the same, regardless of where they are deployed.

- **Greater efficiency**
    >> Containers allow applications to be more rapidly deployed, patched, or scaled.

- **Better application development**
    >> Containers support agile and DevOps efforts to accelerate development, test, and production cycles.

![](./contain.png)


## System Setup

As mentioned in the beginning, we'll be breaking a monolith application into microservices. Prior to this, we'll need to ensure we have access to a few software and tools. Let's get started!

**Step One: Creating an Amazon Web Services (AWS) Account**

If you do not already have an AWS account set up, please create a free one [here](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html). 

![](./awslogin.png)

**Step Two: Installing Docker**

Next, we'll install Docker. Docker is an open-source project for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises. We'll use this to build the image files that will run in our containers. 

Follow either the [Mac](https://docs.docker.com/docker-for-mac/install/) or [Windows](https://docs.docker.com/docker-for-windows/install/) instructions to have this downloaded to your desktop.

![](./docker.png)

Once installed we can verify it is running by entering the following command in the terminal:

    docker --version

The version number should display as below: 

![](./dockerversion.png)

**Step Three: Installing the AWS Command Line Interface (CLI)**

The AWS CLI is what we'll be using to push the images to Amazon ECR. Please follow this [guide](http://docs.aws.amazon.com/cli/latest/userguide/installing.html) to download and learn more about AWS CLI. 

Once downloaded and installed, verify that it is running on your terminal by running:

    aws --version

![](./awsversion.png)

 If you already have AWS CLI installed, run the following command in the terminal to ensure it is updated to the latest version:

    $ pip3 install awscli --upgrade --user

![](./pipe.png)

**Step 4: Downloading a Text Editor for Coding**

If you don't already have a text editor for coding, install one to your local environment! Both [Atom](https://atom.io/) and [Visual Studio Code](https://code.visualstudio.com/) are simple, open-source text editors that are popular with developers.

For today's example, we'll utilize VS Code.

![](./atom.png)

![](./vscode.png)

**Step 5: Downloading the Repository from Github**

If you haven't already created an account with Github, go ahead and do so [here](https://github.com/).

![](./github.png)

Next, log into your account and navigate to the following repo on your web browser: https://github.com/awslabs/amazon-ecs-nodejs-microservices

Select 'Code' and then click 'clone link,' in order to download the GitHub repository to your local environment.

![](./gitrepo.png)

There are two ways to clone your repo:

1. Open up your text-editor and use the 'Clone Repository' tab on the left-hand side. You'll have the option of entering in your cloned URL from github there. You may be asked where on your PC you'd like to save your repository. Once you do so, you will have access to the *amazon-ecs-nodejs-microservices* repository we cloned from Github.

![](./clone1.png)

![](./clone3.png)

2. You can clone the repo to your Terminal, using the following command:

    $ git clone <clone-link>

![](./clone2.png)

**Step Six: Creating the Repository on AWS**


# Part One: Containerize the Monolith

Now that we have everything set up and ready to go, we can now build the container image for our monolothic node .js application and push it to our Amazon Elastic Container registry.