# The Talk

---

SWITCH SLIDE #1

---

Hi guys!

refer to TITLE

but, before we start with the actual presentation let us first introduce ourselves.

---

SWITCH SLIDE #2

---

My name is Jürgen, I am a full time Drupal developer in Fenomen web agency. I 
have about 3 and a half years of experience with Drupal professionally.

My Name is Mait and I work for Fenomen web agency as well. I have been working 
with Drupal a little bit more than a year professionally.

So now that everyone briefly knows who we are, lets talk about Drupal and 
Docker. How can these two technologies work together and why you should care.

Rise your hand if you have used Docker already in your development environment.

Keep your hands up for a moment!

Lower your hand if you have not yet used Docker in production.

Those whose hands are still up, you may already know everything this 
presentation is going to present to the audience, but there is a high chance 
that you don't know everything, so you may still learn something new from this 
talk.

Ok!

So lets start!

---

SWITCH SLIDE #3

---

So what is Docker?

Docker is a piece of technology that allows you, the developer, to wrap your 
application and all of its dependencies that it needs in order to run into a 
standardized package, which you can run in any host.

The only requirement to get your application running in 99% of the time is that 
you also need to have Docker installed on that host.

Because Docker relies heavily on Linux specific features, you can currently run 
Docker natively only on Linux, but there are multiple ways how you can run it 
on non Linux hosts as well.

Docker also gives you tools so you can share your application with others with 
ease.

That is I think the most simplified high level explanation I could think of how 
I would describe Docker to a Drupal developer very briefly.

There is obviously much more to Docker than I have managed to describe in that 
short description, but we will focus mostly on these aspects of Docker in this 
presentation, since these are the most important features that you should be 
familiar with if you want to boost your development experience with Drupal 
using Docker.

---

SWITCH SLIDE #4

---

At the beginning Docker used Linux Containers more widely known as LXC as the 
default execution environment for the backend.

The issue with LXC is that it's heavily dependent on Linux as the name implies.

To solve that particular problem Docker now supports different execution 
drivers so your application in theory could run potentially on any operating system that 
supports operating-system-level virtualization and has a execution driver 
implemented for Docker such as FreeBSD which at this time has an experimental driver 
for Docker.

Docker developers have also developed their own execution driver called 
libcontainer to replace LXC on Linux systems so they could have more control 
over the runtime.

On operating systems that doesn't support operating-system-level virtualization 
you could always fallback to a traditional fully virtualized environments and install for
example a VirtualBox to your machine and run your prefered Linux distribution 
on it, then you have fully virtualized Linux capabilities on your non Linux 
machine.


The problem with plain VirtualBox is that you have to manually set up your 
network and volumes so you could work on your Drupal projects from your host 
comfortably.

Another option is to use 

If this 

https://www.reddit.com/r/docker/comments/38l5as/osx_tip_using_dockermachine_vs_boot2docker/
https://www.reddit.com/r/docker/comments/2osgl7/vagrant_vs_boot2docker/
http://geoffrey.io/what-is-docker.html

---

SWITCH SLIDE

---

What is an image?

A Docker image is a read-only template for your application. Basically an image 
is a collection of files that your application needs in order to run.

It is very similar conceptually to a tarball, which is a collection of files 
and directories which you can move around as a single unit. Docker image is 
exactly like that.

Depending on your application and its dependencies the Docker image can be 
either very small, something around few megabytes, or very large, from a couple 
of gigabytes to infinity in theory.

There are many ways how you can build a Docker image. You can build an image
either by hand or in an automated way.

The problem building an image by hand is that for example if you have already
built an image, you have added all the dependencies that your application 
needs, but you are required to make a change to that image in the future.

For example you may need to update a library that your application is using or 
patch a vulnerabilty.

And lets say a month goes by and the change will not be done by you, but by 
another developer that didn't build this image himself. 

He probably don't have any clue how the image was made and what exactly is 
packed into that image.

So you literally gave him a black box in a sense, which is very hard to work 
with. I'm sure even you, the author of the image probably will not remember how 
exactly you built it yourself.

I guess you guys can see the issue here?

Fortunately there is a better way to do it. Docker is able to build an image by 
reading instructions from a text file. We will be referring to it as Dockerfile 
in this presentaion as that is the offical name for it.

Every time you want to run your application, first you have to deploy your 
Docker image to your server and create a container from it which is the running 
instance of your application.

So the idea that you can put your application and all of its dependencies into 
a single package, and build the package automatically in a repeatable way 
removes so much of the complexity when deploying your application to a server 
or sharing it with other developers.

---

SWITCH SLIDE

---

What is a Dockerfile?



---

SWITCH SLIDE

---

What is a container?

From a developer point of view, a container provides an isolated virtual 
environment for your application.

This means that your application process is securely isolated from other 
processes on the same host.

It can have a separate network interface or share a network interface with 
host's interface or with other containers, you can also control how much 
resources your applications can have on the host. You may want to limit the 
memory consumption to specific value if for example you run multiple containers 
on the same host for the same application.

, CPU, disk space and many more).

You can even limit the disk space that your application could have access to.

Because you have such a fine control of resource allocation, Docker also gives 
you tools to get the necessary metrics for your application, which you can use
to monitor you application.

Containers are very lightweight. You could run hundreds, even thousands of 
containers on a single host, thats how lightweight they are.

At the last DockerCon that took place in couple of months ago in USA, San Francisco
they demod how they managed to run run 250 containers on a Raspberry Pi 2.

https://www.youtube.com/watch?v=MHJmNZSRve0

The underlying techonolgy (namespace isolation and control groups) that Docker 
itself makes use of are actually provided by Linux kernel itself.

---

SWITCH SLIDE

---

A good example in my opinion how it would be easier for a developer to better 
grasp the idea between a Docker image and a Docker container is, if you 
think about the basic concept of object-oriented programming paradigm, which I'm
sure you know well, since most of you here are developers I suppose. If you 
don't know it yet, then Drupal 8 definitely forces you to learn it, which is
a good thing.

In OOP you have classes that specifies the structure of data and the behaviour 
of your objects. It's basically a template or blueprint for your objects.

The same concept can be applied for the relationship between Docker images and 
Docker containers.

Docker image in this case is like a class that contains your application code 
and all of its dependencies and you create containers that are derived from that 
Docker image, which then are created or destroyed on demand just like objects. 

You can share your Docker image with other developers just like you can share
your class that you have written as a text file, but you can't share Docker 
containers because they are the running instances of that image just like 
objects.

But just so you know, in the future you actually could send a running container 
from one host to another by creating a full snapshot (memory dump, mutable data 
etc.) from the container, but this feature is still in an experimental phase.

There is a video from the last DockerCon on YouTube in the official Docker 
channel where the guys are demonstrating this functionality.

---

SWITCH SLIDE

---

What problems does it solve?

---

SWITCH SLIDE

---

So how did we end up using Docker in our development environments?

The timing was perfect, because one of our developers ruined his whole development environment by changing all the files and directories permissions to apache

    sudo chown -R www-data.www-data /

---


so now that everyone are prepared for what comes next, let's start the presentation

Exactly a year ago I found this tool called Docker.

After playing with it some time, it blew my mind, because never before I would have been imagined that creating isolated environments
for applications and services could be so fast and intuitive.

I've always liked the idea of virtualization, but at the same time it has always been somewhat heavy in terms on resources it needs for running and starting a virtualized machine takes too much time that it’s not 

The fact that I now have almost 4000 commits in GitHub shows that I have discovered something awesome that is worth the time to invest in.

Docker skyrocketed my productivity immensely. It molded my thinking in a way that

From that day on I never


## Backlog

Why have we decided to use Docker in our work environment?

Support for different platform

What problems Docker solves and what problems Docker introduces (multiple developers)

A developer 90% of the time doesn’t event relize that he/she is working woth Docker while developing in Drupal.

The famous matrix of hell.

You should alwasy include third party libraries etc to your Docker project

Presentation link at the start of the presentation

Just Do It reference :), don't choke random slides

As of this summer Docker announced that they will be donating parts of its plumbing to The Open Container Project which is hosted by The Linux Foundation and is supported by the industry leaders around the world. The mission of The Open Container Project is to create open industry standards around container formats and runtime. The war is now officially over, which means you can invest in Docker.

## Questions and answers

Make sure to write down any unanswered questions and get back to the questioner as soon as you have the answer. Don't forget to ask them contact details!