# The Talk

Hi guys!

Before we start with the actual presentation let us first introduce ourselves.

---

SWITCH SLIDE

---

My name is Jürgen, I am a full time Drupal developer in Fenomen web agency. I 
have about 4 years of experience with Drupal professionally.

My Name is Mait and I work for Fenomen web agency as well. I have been working 
with Drupal a little bit more than a year professionally.

So that now everyone knows briefly who we are, lets talk about Drupal and 
Docker. How can these two technologies work together and why you should care.

Rise your hand if you have used Docker already in your development environment.

Do not lower your hands just yet!

Lower your hand if you have not yet used Docker in production.

Those whose hands are still up, you probably won't learn anything new from this 
talk, so you may stand up and walk out. I'm just kidding guys! Nobody knows 
everything, so you actually might learn something from this presentation after 
all.

We at least hope that you do.

---

SWITCH SLIDE

---

So what is Docker?

Docker is a piece of technology that allows you, the developer, to wrap your 
application and all its dependencies that it needs in order to run into an 
image, which you can run in any host.

The only requirement to get your application running in 99% of the time is that 
you also need to have Docker installed on that host.

Depending on your application and its dependencies the Docker image can be 
either very small, something around few megabytes, or very large, from a couple 
of gigabytes to infinity in theory.

Docker also gives you tools so you can share your image with others with 
ease.

---

SWITCH SLIDE

---

What is an image?

A Docker image is a read-only template for your containers. 

---

SWITCH SLIDE

---

What is a container?

From a developer point of view, a container provides an isolated virtual 
environment for your application.

This means that your application process is completely isolated from other 
processes on the same host.

It can have a separate network interface or share a network interface with host 
or with other containers, you can also control how much resources your 
applications can have on the host. You may want to limit the memory consumption 
to specific value if for example you run multiple containers on the host for 
the same application.


, CPU, disk I/O and many more).

Because you have such a fine control of resources that can apply for your 
application you can also get all the necessary metrics for you application.

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
and all its dependencies and you create containers that are derived from that 
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

What problems Docker solves and what problems Docker introduces

A developer 90% of the time doesn’t event relize that he/she is working woth Docker while developing in Drupal.

The famous matrix of hell.

## Questions and answers

Make sure to write down any unanswered questions and get back to the questioner as soon as you have the answer. Don't forget to ask them contact details!