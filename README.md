# Infer-Windows-Setup
This guide will walk you through the steps to install `facebook/infer` on Windows using Docker

### 1. Prerequisites
- Make sure that you have Docker installed on your Windows machine. If this is not the case, here is the [link](https://docs.docker.com/engine/install/) on how to install Docker Desktop for Windows.
- Next start the Docker Desktop application. When Docker is up, you should see a panel with the status 'Docker is running'

### 2. Create a Ubuntu container and install some packages
- Open a command prompt and run this to create a Ubuntu container.
```
docker run --name ecse429 -it ubuntu /bin/bash
```
- The above command will pull the `ubuntu:latest` image and instantiate a Ubuntu container with the name `ecse429` out of it. When the command finishes executing, you should see something like this:
```
root@1d91467395a8:/#
```
- This indicates that you have logged in the container as a `root` user. Now, you can go ahead and install some packages such as java JDK, maven, git, etc.
- Install `JDK 11` on the container and verify that the package is installed successfully
```
apt update
apt install default-jdk
java --version
```
- Install `Maven` and verify that it is installed successfully
```
apt install maven
mvn --version
```
- Install `git`
```
apt install git-all
git --version
```
- You should now be able to install `infer` and start working with it

### 3. Install Infer and run an analysis
- Install `curl`
```
apt install curl
```
- Follow this [instruction](https://fbinfer.com/docs/getting-started) on how to install Infer v1.1.0(latest) on a linux machine. Note that you don't have to use `sudo` command since you are logged in as the `root` user
- Verify that infer is installed
```
infer --version
``` 
- The next step is to run Infer analysis on a repository
- Clone a github repository of your choice and `cd` into it
- Run Infer analysis with Maven on this repo
```
infer run -- mvn compile
```
- You should be able to see an analysis made by Infer when the command finishes executing

### 4. Exit and save the container
- When you finish your work, exit the container by running the command `exit`. Note that you should not delete the container if you are planning to work with infer multiple times later on
- When you want to continue the work, just go to the Docker Desktop panel and restart the container `ecse429`. Then run this command to log into the container
```
docker exec -it ecse429 /bin/bash
```
