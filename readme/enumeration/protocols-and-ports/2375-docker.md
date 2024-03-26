# 2375 - Docker

## Theory

Docker is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers. The service has both free and premium tiers. The software that hosts the containers is called Docker Engine. It was first released in 2013 and is developed by Docker, Inc.

The main components of Docker are:

* **Docker Client:** The Docker client is a command-line interface (CLI) tool that allows you to interact with the Docker daemon. You can use the Docker client to build, run, and manage containers.
* **Docker Daemon:** The Docker daemon is a background process that runs on the host machine. It is responsible for building, running, and managing containers.
* **Docker Image:** A Docker image is a read-only template that contains everything needed to run an application. Docker images are stored in a Docker registry.
* **Docker Registry:** A Docker registry is a repository for storing Docker images. Docker registries can be public or private.
* **Docker Container:** A Docker container is a running instance of a Docker image. Containers are isolated from each other and from the host machine.



***

## Practical

### Basic Nmap Scan

```
nmap ‐sV ‐p 2375 ‐T5 172.16.0.100
```

### NSE Scan

```
nmap ‐sV ‐O ‐‐script=docker* ‐p 2375 ‐T5 172.16.0.103
```



***

## REFERENCES

* [https://docs.docker.com/](https://docs.docker.com/)
* [https://l3m0n.gitbook.io/pen-testing-book/container-pentesting/docker-pentesting](https://l3m0n.gitbook.io/pen-testing-book/container-pentesting/docker-pentesting)
* [https://book.hacktricks.xyz/network-services-pentesting/2375-pentesting-docker](https://book.hacktricks.xyz/network-services-pentesting/2375-pentesting-docker)
* [https://blog.ropnop.com/docker-for-pentesters/](https://blog.ropnop.com/docker-for-pentesters/)
