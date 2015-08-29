# drupalcamp-baltics-2015

# Using Docker to boost your development experience with Drupal

---

![SWITCH TO SLIDE #01](https://raw.githubusercontent.com/dockerizedrupal/drupalcamp-baltics-2015/master/slides/SWITCH%20TO%20SLIDE%20%2301.png "SWITCH TO SLIDE #01")

---

Hello guys!

My name is Jürgen.

My name is Mait.

We are two ordinary Drupal developers from a compnay called Fenomen who has 
never given a speech before.

I'll start by saying that our English is not that fluent as you would expect 
from an ordinary guy that gives presentations at conferences.

Because we have a quite a large amount of topics to cover and the amount of
time that have been given to us to perform this presentation is finite, we have
left no room for any improvisation and would gladly use this little assistant 
called Kindle as our guide today.

So we hope that you don't mind because the topic in our opinion is quite 
interesting.

Now that we have your attention and you know what to expect from this 
presentation, lets talk about Drupal and Docker. How can these two technologies 
work together and why you should care.

---

SWITCH TO SLIDE #02

---

Like most of the presentations out there, we have given a title to this one as 
well, which is "Using Docker to boost your development experience with Drupal".

We have divided this talk into two major parts.

The first part introduces Docker, what exactly is it and how it works. On 
second part we will be discussing how we at Fenomen ended up using Docker and 
what problems it helped us to solve when developing Drupal based projects.

This presentation is primarily meant for beginners in general, but we are 
hoping that some of you who think that they already know Docker, still might 
learn something new from this talk.

---

SWITCH TO SLIDE #03

---

So what is Docker?

Docker is a piece of technology that allows you, the developer, to wrap your 
application and all of its dependencies that it needs in order to run into a 
standardized package, which you can run virtually in any host.

The only requirement to get your application running in 98% of the time is that 
you also need to have Docker installed on that host.

Because Docker relies heavily on Linux kernel specific features, you can 
currently run Docker natively only on Linux, but there are official and 
unofficial ways how you can run it also reasonably well on non Linux hosts.

Docker also gives you tools so you can share your application with others with 
ease.

That is I think the most simplified high level explanation I could think of how 
I would describe Docker to a Drupal developer that has never used 
Docker before.

There is obviously much more to Docker than I have managed to describe in that 
short description, but we will focus mostly on these aspects of Docker in this 
presentation, since these are the most important features that you should be 
familiar with if you want to boost your development experience with Drupal 
using Docker.

---

SWITCH TO SLIDE #04

---

Docker only runs natively on Linux, however not everyone is using Linux today 
as their primary development environment.

Fortunately, there are multiple options for running Docker on a non Linux 
host.

The most portable and flexible way to use Docker on non Linux hosts is to use 
whole-system virtualization technology. 

Our personal favourite is VirtualBox that allows you to create and manage
virtual machines in my opinion very beginner friendly way.

It can run on many different operating systems and supports large number of 
guest operating systems including Linux.

The primary downside using plain VirtualBox or any other hypervisor is that you 
have to do most of the initial configuration yourself manually.

Normally developers are not interested in wasting their time configuring their 
environment, but instead they just want to get their development environment up 
and running as fast as possible so they could start working on their project.

So just using VirtualBox to run Docker may not work for everybody.

---

SWITCH TO SLIDE #05

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

SWITCH TO SLIDE #06

---

The official and recommended way to get started with Docker is to use very 
recently announced tool called Docker Toolbox.

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
Docker ecosystem on that platform is superb.

---

SWITCH TO SLIDE #07

---

The architecture of Docker in a nutshell, in context of this presentation,
consists of two primary parts, Docker Engine and Docker Client.

Docker Engine is basically a daemon that runs continuously on your machine as a 
service. Docker Client is a command line tool that a developer can use to 
interact with Docker Engine.

Because Docker Engine and Docker Client can speak TCP to communicate with each 
other, these two programs don't have to be running on the same machine, which 
gives you a flexibility to run and manage your Dockerized applications very 
conveniently on remote machines over the network.

This same flexibility allows you to use Docker very seamlessly for example on 
Mac or Windows.

Despite that, that Docker Engine can run only on Linux, you can still run it in 
Linux based virtual machine and since Docker Client doesn't depend on Linux 
kernel specific features like Docker Engine does, there are binaries for Docker 
Client that you can run directly on Mac or Windows.

So when a developer interacts with Docker Engine on Mac or Windows, he still 
has a sense of feel that the host he is using can run Dockerized applications 
natively.

---

SWITCH TO SLIDE #08

---

So what makes Linux so special that Docker Engine can run natively only on that 
operating system at this time?

Some of you may know that Docker is a containerization technology. In other 
words it means that your Dockerized applications also known as containers are 
running in isolation from other processes on the same machine.

The isolation is done by the host's operating system kernel itself and not by 
some other piece of software like in case for virtual machines where the 
hypervisor is in the role that isolates your guest operating system from the 
rest of the system.

However, not all mainstream operating systems today are supporting 
container-based virtualization.

We look at you Mac and Windows.

So our theory is that since Linux is considered a mainstream operating system 
in the technology world and the Linux kernel does support container-based 
virtualization, then the only logical conclusion is that there were no other 
feasible options available to choose from.

Then you might ask, what about operating systems like FreeBSD and Solaris that 
are also supporting this container-based virtualization concept?

I'm pretty sure that in the future these operating systems will be supported by 
Docker natively, because Docker has been built in a way that it supports 
switching between different execution environments.

Basically you can write an execution driver for Docker Engine for your 
operating system if it has some kind of containerization primitives in place 
that would allow a process to run in a sandboxed environment.

As far as I know there already is an execution driver available for FreeBSD 
that utilizes the Jails mechanism on that platform to isolate processes, 
although it's still considered as an experimental project.

And also Microsoft has started to understand the importance of containerization 
technology by adding containerization primitives to the Windows kernel, which 
currently are only available in the just released Windows Server 2016 Tech 
Preview 3. So expect to be able to use Docker on Windows in the future as well.

---

SWITCH TO SLIDE #09

---

From a developer point of view, the two primary advantages of container-based 
virtualization over whole-system virtualization is the efficiency, how many 
applications you can run in parallel on a single machine, and the speed, how 
quickly you can start and rebuild your application.

A typical virtual machine is usually a couple of gigabytes in size, it takes  
minutes to start and many more minutes to rebuild it from scratch. The 
overhead you have when running your application in a virtual machine is much 
larger than running it on your host natively.

The amount of virtual machines you can run on an average laptop is relatively 
low. I would say if you try to run more that ten virtual machines on your 
laptop then you may already start experiencing performance degradation.

For a developer these numbers are not that appealing and because of that they 
usually run their development tools directly on their host because it's faster.

However, by doing so, they lose some of the flexibility over their development 
environment. The whole point of isolation that virtual machines or containers 
can provide you, is that you can have the same set of tools with different 
configurations and versions seamlessly on the same machine without ever 
conflicting with each other. And this is why some people are still willing to 
use virtual machines to develop their projects, because the benefit they can 
get from isolation outweighs the performance impact that using virtual machines 
have on their system.

These are the exact issues that you can solve by using containers instead of 
virtual machines for development.

The primary disadvantage of container-based virtualization in practice is that 
you can not run applications in containers that are compiled for a different 
operating system as your host. For example you can't run Windows based 
executables directly in a container if your host operating system is Linux. 
There is no such limitations for virtual machines.

Using containers mostly wouldn't be a problem for a Drupal developer, because 
most of the third party services that are usually used in along side with 
Drupal are able to run on Linux anyways.

---

SWITCH TO SLIDE #10

---

Now that you have a better understanding of some fundamentals that enables 
Docker to do its work, we are going to explain you next some of the internals 
about Docker in more detail.

One of the building blocks of Docker is the concept of image.

A Docker image is a read-only template, which in simply put is a collection of 
files that your application needs in order to run.

For example an image could contain a Linux distribution like Debian with Apache 
and your Drupal project files.

It is very similar conceptually to a tarball, which is a collection of files 
and directories which you can move around as a single unit.

Depending on your application and its dependencies the Docker image can be 
either very small, something around few megabytes, or very large, from a couple 
of gigabytes to infinity in theory.

Docker images can be pushed into a centralized registry where other parties can 
easily pull it to their machine.

There are several companies that are providing public and private registries on 
the internet today. Docker, a company behind the Docker project also provides a 
public registry to everyone to use for free and a private registry for a fee.

The name they have given to that service is called Docker Hub.

I definitely recommend you to use Docker Hub if you need to make your images 
easily accessible to others.

Docker registry is also available as an open source software, so you can set up
a private registry relatively easily on your own server.

Using a registry requires usually access to a network, so in case where your 
machine is not virtually able to communicate with a registry, there is always 
an option to export an image to a file, which you can move around through other 
mediums.

---

SWITCH TO SLIDE #11

---

There are a couple ways how you can build a Docker image. You can build an 
image either by hand or in an automated way.

The problem building an image by hand is that for example if you have already
built an image by executing a series of commands on top of each other and you 
are required to make a change to that image in the future.

For example you may need to update a library that your application is using or 
patch a vulnerability for a third party service.

And lets say several months goes by and the change will not be done by you, but 
by another developer that didn't build this image himself. 

He probably don't have any clue how the image was made and what exactly is 
packed into that image, because there is no history nowhere to be found that 
would tell him the exact steps that were executed to build this image.

Of course you can always document them to somewhere, but it would still be hard 
to manage, especially if there are hundreds of commands that were needed to 
perform to build this image.

So in a sense you literally have given him a black box, which is very hard to 
work with. I'm sure even you, the author of the image probably would not 
remember how exactly you built it yourself.

Although in some use cases you may not have a choice and you have to build or 
extend an image manually, nevertheless there is a better way to build a Docker 
image.

Docker is able to build an image by reading instructions from a text file. The 
official term for that is Dockerfile.

We will not be covering the manual process in this presentation, because 
honestly we personally have not had a reason to use it in practice.

---

SWITCH TO SLIDE #12

---

Another important concept in Docker is a container. Without understanding the 
basics of it, it's very hard to understand how Docker works.

From a developer point of view, a container provides an isolated virtual 
environment for your application that feels like a lightweight virtual machine.

But architecturally they still are different virtualization concepts.

This means that your application process is virtually isolated from other 
processes running on the same machine.

From an application point of view, there is a little or no difference when 
running your application inside or outside the container. The inside looks most 
of the time the same like outside.

Sharing the host's operating system kernel with other containers, allows your 
application to be more efficient, but still giving you virtual machine like 
capabilities.

Containers are created from Docker images. 

In some cases for example you may need to debug a service that is running 
inside the container, then Docker is able to give you a shell to a running 
container.

A container can have a separate network interface or share a network interface 
with host's interface or with other containers. You can also control how much 
resources your applications can have on the host. You may want to limit the 
memory, CPU or disk space consumption to a specific value if for example you 
run multiple containers on the same machine.

Because you have such a fine control over resource allocation, Docker also 
gives you tools to get the necessary metrics for your application, which you 
can use to monitor you application performance.

Containers are very lightweight. You could run hundreds, even thousands of 
containers on a single host. You definitely can't do that with virtual 
machines.

Starting a container takes most of the time only a couple seconds or less. 
Usually the application or service running inside the container takes more time 
to start than the container itself.

---

SWITCH TO SLIDE #13

---

For some of you the concept between a Docker image and a Docker container might 
still be a bit unclear.

I once had to explain this to another Drupal developer that also didn't get the 
concept right away.

So the alternative explanation I gave him helped him to better understand it.

Most of you here are PHP programmers, at some time you probably have acquired 
some knowledge about object-oriented programming.

Try to think about the most basic concept of object-oriented programming 
paradigm where you have a class and an object.

A class is a blueprint, which specifies the structure of data and the behaviour 
of your objects.

The same concept can be applied to the relationship between a Docker image and 
a Docker container.

Docker image in this case is like a class that contains your application code 
and all of its dependencies and you create containers that are derived from 
that Docker image, which then are created or destroyed on demand just like 
objects in PHP. So you can run multiple containers from a single image with 
different arguments to modify your application or container behaviour on 
runtime.

You can share a Docker image with other developers as easily as you can share
a class that have been written to a text file.

Just so you know, in the future you could also share a running container with 
others by being able to create a full snapshot from it, but this feature is 
still in an experimental phase.

---

SWITCH TO SLIDE #14

---

I don't want go into much detail about explaining you everything there is to a 
Dockerfile, because most of that you can easily find on the official Docker 
website.

However, to get some better idea how Docker works we still need to give you 
some basic understanding of it.

Dockerfile in a way is a blueprint for your Docker image.

It's a simple text file that contains a series of instructions on how to build 
an image.

If you are familiar with Linux command line interface then you basically 
already know how to write a Dockerfile.

The only key difference between executing a command directly in a terminal and 
in a Dockerfile, is that, a command in a Dockerfile doesn't expect you to 
interact with it during the image building process.

So you have to construct your command that expects an input form a user during 
runtime in a way that all the input that your command needs are directly piped 
to that command in advance or using command line flags to make choices if a 
particular command supports it.

---

SWITCH TO SLIDE #15

---

A good example to illustrate this is installing Apache thought a Debian package
management system. By default if you install a package with apt-get install 
without adding any extra flags you will be prompted to make a choice, either 
you can cancel the operation or continue with the installation process.

But if you would let Docker Engine to execute the same command from a 
Dockerfile, the build process would fail immediately, because it's fully 
automated and doesn't expect any interaction from a user.

By adding -y flag to your apt-get install command, a package will be installed 
without first asking your confirmation.

---

SWITCH TO SLIDE #16

---

This is how a simple Dockerfile looks like.

You can build a Docker image from it, that installs Apache on top of Debian 
file system and it replaces the contents of the default index.html file with 
the sentence "Hello, DrupalCamp Baltics 2015!".

As you can see the format of a Dockerfile is very simple.

On the first line you have a simple comment that is there to give you some 
insight about the Dockerfile.

On the second line at the left you have an instruction usually in uppercase, 
like in this case the keyword FROM and to the right you have arguments for that 
instruction.

Every other line in Dockerfile expect the comments are following the same 
pattern.

So let's look into more detail about some instructions that are more important 
in this example.

The second line tells Docker Engine what is the base image that your new image 
will be built upon. In this example it will be the official Debian image, which 
contains the files and directories which Debian itself is made out of.

If a base image doesn't exist on your host at the time of building the image, 
it will be automatically pulled from the Docker Hub or from a private registry.

You can use every other Docker image as your base image. This gives us the 
flexibility to reuse already built images and increase the efficiency of the 
image building process.

On line eight, eleven and fourteen, we see the RUN instruction, which is the 
most common instruction in the Dockerfile. RUN instruction executes a command 
and commits the change to file system back into your image.

If you have not yet noticed then you can see that on line eleven we execute
apt-get install with the -y flag, so the build process wouldn't be interrupted.

The last instruction is the entrypoint for your container. In this example 
Apache will be started in the foreground if you launch the container. As long 
as the resulting process lives, the container will also stay running. If the 
process is killed inside the container, the container will also stop.

---

SWITCH TO SLIDE #17

---

Now that we have covered most of the basics there is to Docker, so you would be
able follow the rest of the presentation, we are going to show you a small demo 
where you can see the Docker image building process in action.

---

PLAY DEMO VIDEO #01

---

So there you go, in this little demo we built a Docker image and started
a container.

Inside the container, Apache process were started on port 80.

We also saw, that making a HTTP request to the loopback address through the web 
browser, we got the actual response form the web server with the right payload.

An action that only took about a minute to perform in practice took nearly 
half an hour to explain. So this should give you some idea how powerful it is 
to have a Docker in your development environment toolbox.

---

SWITCH TO SLIDE #18

---

With this little demo we have finished the first part of our presentation.

We will now going to talk about why and how we at Fenomen switched our 
development environments from native LAMP setup to Docker to develop Drupal 
based projects.

Maybe you are right now experiencing the same problems as we did in our 
development workflow before discovering Docker and our experience using and 
deploying Docker within our team would give you some insight how to resolve
them.

---

SWITCH TO SLIDE #19

---

Before deploying Docker to our development environments the setup we had was 
not very efficient and scalable when working in a team environment.

Our team is relatively small and the amount of projects each our developer has 
to work on or maintain at any given time is quite large.

Imagine having to work on more than 5 different projects on a single day. And 
more than half of those aren't even developed by you, so the time you would 
need to put into getting each project up and running on a native LAMP setup 
can be quite large.

Some projects may also be a couple of years old and getting the right tools to
work on a newer operating system may also be difficult.

A bug that would be normally resolvable by any Drupal developer because the 
nature of the bug itself doesn't require a high level of skill, might 
still be too difficult for a junior developer to fix, because he may lack the 
knowledge and the know-how needed to set up the project on his machine.

Our experience has shown that most who are affected directly by using this 
set up are front-end developers, because if they start to set up a bit more 
complex project by their own, they immediately get stuck. Because the area of 
expertise you need to have to work on your task doesn't belong directly to a 
front-end developer's domain.

As you can see there are many issues using this kind of a set up and processes 
in that work environment. 

---

SWITCH TO SLIDE #20

---

If I'm honest with you, then the real reason why we ended up using Docker 
in our development environment was actually by accident. To get a better idea 
what I mean by that, I'm gonna tell a little story.

Last year in October one of our junior developers was working on a project. 
 
He found out that the file permissions for a project he was working on were 
incorrect.

And he thought that he could safely resolve them by himself.

But unfortunately at this time everything didn't go as well as he planned.

When he realized that his system wasn't working properly anymore he notified a 
fellow colleague for a help.

After some investigation what exactly had happened to his system, we found out 
that the command he entered was following - POINT AT SLIDE.

Processes running on his host were not able to properly access files and 
directories anymore.

At first we tried to recover as much as possible by hand so he could at least 
continue with his work for the day.

But, the damage was already done.

So the only choice we had, was to reinstall the operating system, install and 
configure all the tools that he needed in order to be able to continue with his 
work.

The time that a company had lost from two developers that weren't able to write 
code for the rest of the day, was pretty huge.

If we would had a proper process in place that would have allowed us to build 
and configure everything automatically the impact to the cost would have been 
much smaller.

Learning from this real experience how things shouldn't be done, we started 
thinking about how to solve this problem. How to make our development 
environments more efficient.

We learned that Jürgen had already played with Docker in his free time for some 
time now.

By hearing him out, we came to the conclusion that trying to use Docker to 
make our development environments more efficient could actually work.

So we came up with a plan to divide the process of deploying Docker over time 
to our development environments into two phases.

---

SWITCH TO SLIDE #21

---

In phase one, without first introducing large changes to our development 
workflow, we concentrated only on eliminating the problem we had when something 
would happen to your development machine and it couldn't be recovered easily.

The first thing we did, we moved all the services like Apache, MySQL, PHP 
etc., that were running on a developer machine natively into separate Docker 
containers.

Every Drupal project shared the same Apache, MySQL and PHP container instance.

The other critical part to get right was Drush.

How can we use it in a relatively comfortable way with containers, because it's 
installed along side with PHP service into the same image. If a developer 
wants to use Drush in a containerized environment, he first has to go inside 
the PHP container, find the Drupal directory and execute Drush commands there.

---

SWITCH TO SLIDE #22

---

To solve that, we have created a simple tool called Crush. 

You can install Crush directly onto your host and use it exactly like you 
would use native Drush implementation.

Under the hood by executing a Crush command, it first tries to detect if your 
PHP container is running, if it isn't, it will ask you if you want to start 
it.

Then it tries to identify if the directory you where executing your command is 
inside the Drupal directory tree and if so it does some magic and executes the 
right Drush command inside the container.

From a developer point of view, most of the time he doesn't even notice that 
Docker is the underlying technology that drives his project when using Crush.

Since you can say that Crush in some sense is a version agnostic wrapper around 
Drush then you can use any version of Drush inside the container.

For example, you have to still support an old Drupal 6 project which for some 
reason can only run on PHP 5.2 then the only choice you have is to use Drush 
version 5 or lower.

---

SWITCH TO SLIDE #23

---

The second issue that we had to resolve was networking. How to make it enough 
transparent for the ordinary Drupal developer that he could still develop his 
projects without knowing how exactly Docker networking works.

As you may know by default when you link multiple Docker containers together 
they don't share the network interface with each other. It means that every 
containerized service in your stack lives in a separate network.

Which we think, is a good property to have in a long run.

It solves problem when two or more random services wants to use the same port, 
but they each have a separate network then we don't have to be worrying about 
port conflicts.

Your project can scale more easily in that way.

We found this tool called socat and built it into our PHP Docker image.

It allowed us quite easily to redirect traffic from one network interface to 
another.

So in our case if the developer wants to communicate from PHP with an external 
service like MySQL that lives in a separate container and belongs to a 
different network, he still can use loopback address to communicate with that 
service. So from a developer point of view everything regarding networking 
feels like all the services are still living in the same network.

You should know that socat is not perfect in all cases, because it runs in user
space and not in kernel space it can introduce a noticeable performance hit to 
your project.

So in case if your Drupal project is using lots of modules that are relying 
heavily on database, like Views, Panels, Organic groups etc, it may run 
significantly slower.

Once these two major issues were resolved we started deploying Docker solution 
to our developers machines that were willing to try it out and test.

The feedback we had collected from them was very useful and after fixing some 
minor issues we already saw improvements from using Docker in our work 
environment.

For example if one of the developers found a useful service or a tool that 
could improve his daily work, he made an image out of it and by doing so he 
immediately could share it with other developers that were using Docker and it 
worked everywhere exactly the way.

Another example where we had a real opportunity to test it out was when a new 
developer joined with our team.

Instead of preparing the machine for a development a day before his arrival we 
did it at the same day within 45 minutes which also included installing the 
operating system and giving him a small lecture about the environment. Which is 
a tremendous improvement from our previous approach to solve that problem.

---

SWITCH TO SLIDE #24

---

But we didn't stop there and here is where the phase two comes in.

We found a tool called Fig which allows you to specify the configuration of a 
multi-container application in a single YAML file.

Today Fig is deprecated and is replaced with an official tool called Docker 
Compose.

Instead of sharing Apache, MySQL and PHP container instances between all
projects on a developer machine, Docker Compose allowed us to use project 
specific containers. 

This is very useful architectural change primarily for one thing.

When your drupal project is different from the rest of the projects and it 
needs different or customized services to be able to run. With a shared 
environment it's pretty complicated to maintain the differences between your 
services that are running your projects.

For example, your project might need a Redis support from PHP, if you are 
sharing a PHP container with all your projects, then all your projects will 
also have a support for that version of Redis, but what if another project 
needs an older version of Redis or whatever other service or tool in order to 
work. 

So managing a shared system where you absolutely have to use project specific 
containers, becomes extremely hard.

Removing the shared system all together and using an architecture where you 
only have project specific containers running on your machine, with Docker 
Compose is very easy to achieve.

But to make that system efficient you need to have some services and tools in 
place to support it.

---

SWITCH TO SLIDE #25

---

Since you could have hundreds of containers running simultaneously on your 
development environment you need a way how to directly access them without 
wasting much time searching for them.

The first tool we developed was vhost that itself runs inside a container. 

The purpose of this tool is to constantly monitor your development environment 
and generate a list from all your running containers which are displayed on a 
single web page that you can access with your web browser on port 80 or 443. 

Under the hood inside the container runs Nginx that dynamically generates its 
configuration from the events that are emitted by the Docker Engine. So if a 
container dies it will be removed from the Nginx configuration and if a new 
container is launched a new entry will be added to the configuration.

So by using this tool all your multi-container Drupal projects running on your 
machine are accessible through DNS. 

Currently vhost doesn't provide DNS service itself.

At Fenomen we are relying on an external service, that does DNS for our 
development machines. But one of our goals is to find a way how to do it 
properly on a local machine, so we don't have to rely on an external service to 
do DNS.

---

SWITCH TO SLIDE #26

---

Another essential tool we have developed to have a good experience working with 
Drupal using Docker is called Drupal Compose.

The goal of this tool is to allow you to easily generate Docker 
Compose YAML files for your Drupal 6, 7 and 8 projects automatically. So you 
can start developing your normal Drupal projects immediately that doesn't 
require any specific configuration.

Most of our Docker images configurations can be changed on runtime when you 
launch a container. In practice this means that if a developer for example 
needs to allocate more memory for his Drupal project he can do this directly in 
the Docker Compose YAML file, so he doesn't need to create another project 
specific PHP image just to change a memory limit.

---

SWITCH TO SLIDE #27

---

The final component that we included in our setup was a private Docker 
registry.

All our Docker images that are specific to projects are stored there.

We can save a lot of time by building an image only once and pushing it to the 
registry. If every other developer just wants to use that image, they just pull 
it from the registry.

---

SWITCH TO SLIDE #28

---

Let's see how everything we have talked about in the second part of this 
presentation works in practice.

---

PLAY DEMO VIDEO #02

---

In this video we saw how the developer downloaded the Drupal source code to his
machine, created a standard Docker Compose YAML file for his project and
started the containers with Crush.

By using vhost he was able to access Drupal and PhpMyAdmin easily via the web 
browser.

The last command was there just to verify if Drush was able to communicate with 
Drupal as well.

---

SWITCH TO SLIDE #29

---

By using Docker our efficiency in terms of time and productivity has gone up 
greatly. Our developers are enjoying the development workflow that Docker can 
provide to them.

---

SWITCH TO SLIDE #33

---

Everything we have talked about in this presentation, including this exact
presentation can be found at docerizedrupal.com, feel free to use this material
freely and please contribute if this topic also interests you, so we can make it
together even better.

---

SWITCH TO SLIDE #31

---

Thank you

## License

**MIT**
