# Introduction to Containers 

The idea of a container is to give : 
- the independent scalability of workloads in PaaS
- an abstraction layer of the OS and hardware in IaaS.

A configurable system lets you `install your favorite runtime, web server, database, or middleware, configure the underlying system resources, such as disk space, disk I/O, or networking, and build as you like`.

## What is a container ? 
- an invisible box around your code and its dependencies
- with limited access to its own partition of the file system and hardware
- requires a few system calls to create and it starts as quickly as a process
- only need an OS kernel that supports containers and a container runtime
- so the OS is being virtualized, it scales like PaaS but gives you nearly the same flexibility as IaaS.
- So you can go from development, to staging, to production, or from your laptop to the cloud, without changing or rebuilding anything.

## More information 
### How to build your applications using lots of containers, each performing their own function like microservices ?
If you build them this way and connect them with network connections, you can make them modular, deploy easily, and scale independently across a group of `hosts` (single host if it's just one mcs).
The hosts can scale up and down and start and stop containers as demand for your app changes or as hosts fail.