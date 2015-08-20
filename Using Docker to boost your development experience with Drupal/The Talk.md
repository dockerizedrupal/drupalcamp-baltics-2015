# The Talk

---

SWITCH SLIDE #1

---

Hello guys!

My name is Jürgen, I'm a full time Drupal developer at Fenomen web agency. I 
have about three and a half years of experience with Drupal professionally, but 
unfortunately at the same time I don't have any real experience sharing my 
knowledge and opinions publicly to others.

However I like to believe that the fear to fail in front of an audience 
shouldn't be the dictating factor not to do it, because if the goal is to 
improve their own and other people's work, then it's more sustainable to give 
than receive.

So I feel that it's my responsibility to make my first real contribution to 
Drupal community today by giving this small talk with my good colleague Mait.

Hi, my Name is Mait and I work for Fenomen web agency as well. I have been 
working with Drupal a little bit more than a year professionally. Also, this is 
my first DrupalCamp, so I'm very delighted that I have given the opportunity to 
be here in front of you, fellow Drupal enthusiasts.

So now that everyone briefly knows who we are, lets talk about Drupal and 
Docker. How can these two technologies work together and why you should care.

---

SWITCH SLIDE #2

---

Like most of the presentations out there, we have given a title to this one as 
well, which is "Using Docker to boost your development experience with Drupal".

We have divided this talk into two major parts.

The first part introduces Docker, what exactly is it and how it works. On 
second part we will be discussing how we at Fenomen ended up using Docker and 
what problems it helped us to solve when developing Drupal based projects.

Raise your hand if you have already used Docker in your development 
environment.

Lower your hand if you have used Docker in your development environment but 
not yet in production.

You all may now lower your hands.

So for some of you this presentation may be a bit boring because you probably 
already know most of the stuff we are going to address in this talk, since 
using Docker in production in my opinion requires most of the same knowledge 
as you would need to know when using it in a development environment anyways.

Despite that there is a high chance that you don't know everything, so you may 
still learn something new from this talk, because the landscape is still 
changing quite rapidly.

---

SWITCH SLIDE #3

---

So what is Docker?

Docker is a piece of technology that allows you, the developer, to wrap your 
application and all of its dependencies that it needs in order to run into a 
standardized package, which you can run virtually in any host.

The only requirement to get your application running in 99% of the time is that 
you also need to have Docker installed on that host.

Because Docker relies heavily on Linux kernel specific features, you can 
currently run Docker natively only on Linux, but there are official and 
unofficial ways how you can run it also reasonably well on non Linux hosts.

Docker also gives you tools so you can share your application with others with 
ease.

That is I think the most simplified high level explanation I could think of how 
I would describe Docker to a Drupal developer very briefly that has never used 
Docker before.

There is obviously much more to Docker than I have managed to describe in that 
short description, but we will focus mostly on these aspects of Docker in this 
presentation, since these are the most important features that you should be 
familiar with if you want to boost your development experience with Drupal 
using Docker.

---

SWITCH SLIDE #4

---

Docker only runs natively on Linux, however not everyone is using Linux today 
as their primary development environment.

Fortunately, there are multiple options for running Docker on a non Linux 
host.

The most portable and flexible way to use Docker on non Linux hosts is to use 
whole-system virtualization technology. 

My personal favourite is VirtualBox that allows you to create and manage
virtual machines in my opinion very beginner friendly way.

It can run on many different operating systems and supports large number of 
guest operating systems including Linux.

The primary downside using plain VirtualBox or any other hypervisor like that
is that you have to do most of the initial configuration yourself manually.

Provisioning a guest operating system may also be a bit overwhelming for some 
people.

Normally developers are not interested in wasting their time configuring their 
environment, but instead they just want to get their development environment up 
and running as fast as possible so they could start working on the project 
effortlessly.

So just using VirtualBox to run Docker may not work for everybody.

---

SWITCH SLIDE #5

---

The other option is to use VirtualBox in combination with Vagrant.

Vagrant has a good support on many mainstream operating systems like Windows, 
Mac and Linux.

I'm sure some of you here already are using Vagrant today, but are probably 
provisioning the guest operating system with the more widely used provisioners 
like classical shell or more advanced configuration management tools like 
Ansible, Puppet etc.

This is a widely used and working setup to get your development environment 
up and running but since this presentation is mostly about Docker we can take 
a step further and provision the guest operating system and manage Docker on 
it with Vagrant as well, since it has an official provisioner created to 
support Docker.

If you are already using Vagrant, then this option is probably best for you.

---

SWITCH SLIDE #6

---

The official and recommended way to get started with Docker is to use very 
recently announced tool called Docker Toolbox.

It is so new that I personally have not yet had time to battle test it in 
everyday work. It was announced about three weeks ago.

If any of you are familiar with Boot2Docker, then you should know that Docker 
Toolbox is here to replace it and it is suggested that you migrate as soon as 
possible.

Docker Toolbox basically is a collection of tools to help you get started with 
Docker quickly on non Linux hosts. The end goal of these tools is to provide 
you a similar experience and the same functionality as you would expect when 
using Docker directly on Linux.

Unfortunately an essential tool for having a great development experience with 
Docker called Docker Compose doesn't work on Windows, so I don't 
recommend using Docker Toolbox on Windows just yet, but I'm absolutely sure 
that it will be supported on Windows in the future. Until then I would use 
Vagrant in combination with VirtualBox on Windows.

But if you are a Mac user, then Docker Toolbox should definitely be your first 
choice working with Docker, because the support for Docker and other tools in 
Docker ecosystem on that platform is great.

---

SWITCH SLIDE #7

---

The architecture of Docker in a nutshell, in context of this presentation,
consists of two primary parts, Docker Engine and Docker Client.

Docker Engine is basically a daemon that runs continuously on your machine as a 
service. Docker Client is a command line tool that a developer can use to 
interact with Docker Engine.

Because Docker Engine and Docker Client can speak TCP to communicate with each 
other, these two programs don't have to be running on the same machine, which 
gives you a flexibility to run and manage your Dockerized applications very 
conveniently on remote machines.

This same flexibility allows you to use Docker for example on Mac or Windows 
very seamlessly.

Despite that, that Docker Engine can run only on Linux, you can still run it in 
Linux based virtual machine and since Docker Client doesn't depend on Linux 
kernel specific features like Docker Engine does, there is a binary for Docker 
Client that you can run directly on Mac or Windows.

So when a developer interacts with Docker Engine on Mac, he still has te sense 
of feel that his Mac can run Dockerized applications natively.

---

SWITCH SLIDE #8

---

So what makes Linux so special that Docker Engine can only run on that 
operating system natively at this time?

Well, there are couple of reasons for that.

Some of you may know that Docker is a containerization technology. In other 
words it means that your Dockerized applications also known as containers are 
running in isolation from other processes on the same machine.
 
The difference between a container and virtual machine is that 


The next option is to use execution drivers that Docker natively makes use 
of on operating systems that are supporting operating-system-level 
virtualization.

I don't want to go into much further detail on explaining what is the
difference between whole-system virtualization and operating-system-level
virtualization at this time, but the basic idea is that in a whole-system
virtualization you have the whole system virtualized, the operating system
kernel and applications running on it. This allows you to run different
operating systems on your host, for example you can run Windows on Linux and 
vice versa. This functionality is provided by the hypervisor like VirtualBox.

However in operating-system-level virtualization the host's kernel is shared 
with your guest operating system, which means that the virtualization is done 
by host's kernel itself. For that reason operating-system-level virtualization 
is not as flexible as the whole-system virtualization, because you can't run 
for example applications written for Windows on your Linux host.

But the benefit that operating-system-level virtualization gives you is that
your virtualized applications are running natively on your host machine. From 
the performance point of view operating-system-level virtualization doesn't 
need extra resources for virtualizing your application, which means that we can
have a process isolation without any loss to the efficiency at that host.

Unfortunately at this time there are only a couple of drivers implemented for 
Docker and they are mostly for Linux only.
 
The default execution driver for Linux is called libcontainer which utilizes 
the Linux kernel features to provide virtualization for your application.

Since we at Fenomen are using Linux 95% on our machines we are using this option 


This would be also the method you would you if you would run a Linux on a virtual 
machine. The key point here to remember is that dependeing on the driver operating 
system level virtualization only allowes you to run guest operatyng systems the same
as the host. So if you are using libcontainer, then the application you want to run 
with Docker also has to support Linux.

As far as I know there are also a drive available to FreeBSD which is still 
considered experimental project.
 
 and the other 
is 
 
 
 but this feature is currently only supported fully on Linux.

So there are not much to talk about that.

At the beginning Docker used Linux Containers more widely known as LXC as the 
default execution environment for the backend.

The issue with LXC is that it's heavily dependent on Linux as the name implies.

To solve that particular problem Docker now supports different execution 
drivers so your application in theory could run potentially on any operating system that 
supports operating-system-level virtualization and has an execution driver 
implemented for Docker such as FreeBSD which at this time already has an experimental driver 
for Docker.

Docker developers have also developed their own execution driver called 
libcontainer to replace LXC on Linux systems so they could have more control 
over the runtime.

The main disatavage is that not every 


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

And lets say several months goes by and the change will not be done by you, but 
by another developer that didn't build this image himself. 

He probably don't have any clue how the image was made and what exactly is 
packed into that image.

So you literally gave him a black box in a sense, which is very hard to work 
with. I'm sure even you, the author of the image probably will not remember how 
exactly you built it yourself.

I guess you guys can see the issue here?

Fortunately there is a better way to do it. Docker is able to build an image by 
reading instructions from a text file. Docker officially calls it as 
Docekrfile.

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
memory consumption to a specific value if for example you run multiple containers 
on the same host for the same application.

, CPU, disk space and many more).

You can even limit the disk space that your application could have access to.

Because you have such a fine control of resource allocation, Docker also gives 
you tools to get the necessary metrics for your application, which you can use
to monitor you application.

Containers are very lightweight. You could run hundreds, even thousands of 
containers on a single host, that's how lightweight they are.

At the last DockerCon that took place in couple of months ago in USA, San Francisco
they demod how they managed to run run 250 containers on a Raspberry Pi 2.

https://www.youtube.com/watch?v=MHJmNZSRve0

The underlying techonolgy (namespace isolation and control groups) that Docker 
itself makes use of are actually provided by Linux kernel itself.

---

SWITCH SLIDE

---

A good example in my opinion how it might be easier for you to understand the 
relationship between a Docker image and a Docker container is, if you 
think about the basic concept of object-oriented programming paradigm, which I'm
sure you know well, since most of you here are developers I suppose.

If you don't know it yet, then Drupal 8 definitely forces you to learn it, 
which is a good thing.

In OOP you have classes that specifies the structure of data and the behaviour 
of your objects. It's basically a template or blueprint for your objects.

The same concept can be applied to the relationship between Docker images and 
Docker containers.

Docker image in this case is like a class that contains your application code 
and all of its dependencies and you can create containers that are derived from that 
Docker image, which then are created or destroyed on demand just like objects. 

You can share your Docker image with other developers just like you can share
your class that you have written as a text file, but you can't share Docker 
containers because they are the running instances of that image just like 
objects.

But just so you know, in the future you actually could send a running container 
from one host to another by creating a full snapshot (which imcludes memory dump, mutable data 
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

So now that you guys have seen a little demonstration that should give you a better idea 
how Docker works and what should you look for if you want to install it on your machine.

We will now going to talk about why and how we switched our development environments 
from standard LAMP setup to Docker for developing Drupal projects at Fenomen.

And maybe you are experiencing the same issues as we did and our experience 
using Docker could help you resolve them.

If I'm very honest with you, then the real reason why we ended up using Docker 
in our development environment was actually by accident. So you may think now what 
exactly then we tried to fix in our work processes. So to get the better idea, 
let me start with by telling you a little story.

Last year in October one of our junior developers was working on a project. 
Nothing unusual there, but because he was working on a Linux, at that time he 
was not very experienced with it, but he had an issue with the project file 
permissions and he thought that he could safely resolve it by himself, but what 
happened was the opposite.

So the command that he entered into the terminal was following:

    sudo chown -R www-data.www-data /

Yes, you can laugh if you want!

For those who don't know what this command does, it changes every file 
and directory ownership to www-data. The command in this case were executed as 
superuser, which makes it extra dangerous. So the outcome after executing it, 
is that your machine is basically broken, because services running on your 
machine can't properly access files and directories anymore.

So the first thing what he did after he realized that his system was unusable, 
he notified me. At first I tried to recover as much as possible by hand so he 
could at least continue his work for the day, because reinstalling an operating 
system and configuring services would have taken us more time than we had been 
given.

But unfortunately the effort I put into trying to recover the system was not 
enough.

Because the incident happened in the middle of the week, we had only one choice 
to resolve it considering the knowledge that we had at that time. In short, we 
backed up all the necessary files, reinstalled the OS and installed all the 
standard services and tools that a Drupal developer may need in his work.

Properly configured machine took more than half a day to set up, because we are 
using phpfarm on our systems to be able to use multiple PHP versions in 
parallel on a single host and the documentation that we had at that time was not up-to-date 
and didn't work out of the box for Ubuntu, so we had to deal with that as well. 

For the rest of the week we still had to install or configure some of the 
services because we obviously had forgotten to install or configure them all at he 
beginning.

So when the weekend arrived I started to think about the issue more closely and how 
could we resolve it or make it a little bit more efficient, because the current 
manual process for that was too costly. Nobody pays for that kind of work or mistakes.

So fortunately I had already used Docker myself but not for solving that kind
of a problem and the more I thought about it the more Docker made sense to me 
that it's the right tool to make this process more efficient.

The initial plan I had, was to simulate exactly the same workflow that we have been 
using already with the standard LAMP setup. So I created basic Docker images for Apache, 
MySQL and PHP etc and because at that time there was no tool known to me that could 
manage those services running in a separate containers as a single service, I 
created a simple shell script for that as well, which basically allowed user to 
start, stop and retsart the services on his own without knowing Docker at all.

// SILDE images graph

Fast forward to a couple of weeks I had a setup that I was personally happy with. Either Drupal version 6 and 7 projects
were working without any major issues on that environment.

So I migrated my development environment completely to Docker.

But because the plan was to ultimately replace standard LAMP setups for other
developers as well, I still had some work to do, because the current setup
required you to know Docker too much.

So yeah, I started working on resolving these issues.

The first and the most critical issue was Drush. How to use Drush in a 
relatively comfortable way with containers. Let me give you an example.

Without doing anything the workflow would look following, when a dveloper wants to 
use Drush he/she has to enter the PHP container, move to the right directory where 
Drupal is mounted and execute Drush commands there. But this workflow isn't 
that intuitive, because using Drush should be easy and problem-free.

To solve that I have created a shell script, which is a proxy for Drush and you install it 
directly onto your host. This proxy script basically proxies all your Drush commands
to inside the container and also detects if the containers are running and 
if they aren't, it will ask you if you want to start them.

The script has been proven to be working pretty well. Most of the time a developer 
that is using it don't even know that he is using Docker and Drush 
is actually executed inside the PHP container.

The second issue that had to be solved was networking, because every service 
that we used was living in a separate container and they don't share the network 
interface with each other. So if a developer wanted to connect for example to 
MySQL database from his PHP script in this case Drupal, he had to know how Docker 
networking works, but my goal in the first stage was not to introduce Docker to our team but to 
solve the problem with provisioning development environments efficiently. So I 
used this tool called socat in the PHP image, which allows you to relay network 
traffic between two independent channels. So basically what I did was that the 
external services that PHP had to had access to I relayd from PHP container local 
network to other containers, so the developer could use externals services seamlessly 
as if they were living on the same machine (127.0.0.1, localhost etc).

Once these two major issues were resolved I started to migrate Docker based development 
environments to other two developers that were willing to try it after I had 
given them a brief explanation how this can benefit them in the short term and 
in the long term. Fortunately they were agreed to try it.

So now that we had a usable development setup that replaced the standard LAMP 
setup, we had lowered the provisioning from more than half a day to about 45 minutes. 
this includes installing the OS as well.

After a couple of months went by saw other improvements in terms of developing Drupal 
projects besides getting your development environment up and running as fast as possible.

For example, if one of the developers had to use for example a
Memcache in his project, we created a simple Docker image for that and deployed it
to every other developer that were using Docker (at that time there were three os us). This basically gave a developer
that never ever had used or configured Memcached before the possibility to use
it without knowing how to configure it. Which is a very powerful thing to have, 
beacuse no matter what skill level you are, you are able to put your effort more 
into the development part than configuring your environment to make this project work.

In time we had created Redis, PHPmyadmin, Adminer etc images and everyone that 
were using Docker could use them, they
all worked consistently the same way on every developers machine, which made 
debugging problems with Drupal or your environment much easier. Because if you 
fix an issue on developers machine you can deploy it easly to others as well.

So we were using this setup a couple of months more during which we had achieved a very stable environment to work on.
And after some time we discovered this tool called Fig which is now known as Docker Compose and this 
let us solve another issue very easily.

So the main problem with the current setup, where you have a single Apache, 
MySQL and PHP containers shared by all your Drupal projects is for 
example if your Drupal project requires some service or extension that is very 
specific to the project, then you need to 
have some kind of a system in place where you can use project specific Docker 
images. This is because not everything should go into general images.

And Docker Compose allowed us to solve exactly that problem.

So the next logical step was to create a general purpose docker-compose.yml 
file for Drupal 6, 7 and 8 which covers 90% of Drupal project requirements.

Every dockerized Drupal project should have this file, it's the initial developer 
responsibility to make sure that this file exists on every project. 

To make this requirement easier to manage, I've created a simple shell script 
that generates this general purpose docekr-compose.yml file automatically and 
the name for this script is Drupal Compose.

And if the standard docker-compose.yml file is not sufficient enough then it's 
every developer responsibility to make a change to it if he has done some changes 
to environment (creating new Docker images, or setting other parameters for the 
general images etc).

So now that we have a system and a process in place which allows us to define 
project specific environment configurations for our projects, then again no 
matter what is your skill level, you can start working on every Drupal project 
immediately, and you don't have to know the details how some services work for this project.

***cordova sass/less reference

***So we started solving one issue that could have been sovled without Docker as well, 
but by using Docker to solve that we made some great imrpovements in other fields as well.


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

Conclusion - don't take this mission by your own, it will be very hard, try to 
involve your organization into as well so they can support you from the high level, 
but in the end it's worht it because if everyone is doing they work properly 
then your work is also easter due that. Tools like Docker allow everyone to do 
they work better.

Docker hub - lots of official images, encourage to make your own

tsintra example native vs docker setup time

simple lamp (simple days) vs complicated stack (multiple services)

old habbits - nativae sass vs docker sass, how to overcome

docker toolbox

destruction promotes growth

docekr fits perfectly into our current infrastructure, since 95% of our developers 
are using Linux for development.

solomon shykes

## Questions and answers

Make sure to write down any unanswered questions and get back to the questioner as soon as you have the answer. Don't forget to ask them contact details!
