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
either very small, something around few megabytes, or very large, from couple 
of gigabytes to infinity in theory.

Docker also gives you tools so you can share your application with others with 
ease.

---

SWITCH SLIDE

---

What is a container?

Some of you

From a developer point of view, a container provides an isolated virtual 
environment for your application.

This means that your application process is completely isolated from other 
process on the same host, it can have a separate network interface or share a 
network interface with host or with other containers, you can also control how 
much resources your applications can consume on the host 
(memory, CPU, disk I/O and many more).

The underlying techonolgy (namespace isolation and control groups) that Docker 
itself makes use of are actually provided by Linux kernel itself.

---

SWITCH SLIDE

---

What problems does it solve?

---

SWITCH SLIDE

---

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