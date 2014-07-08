# ZenOracles - Dockerized Orisi Oracles

Orisi is a distributed system of anonymous oracle nodes which safely validates distributed contracts which use external state for their conditions. More here -> https://github.com/orisi/wiki/wiki/Orisi-White-Paper

## Why Orisi and Docker?

* We need a way to separate __dev-ops__ code from Oracle/Client codebase
* We need to be able to __automate__ and __optimize__ build process
* There must a simple and fast way to use it on multiple __hardware__ or __IAAS__ platforms
* There must be a __oneliner__ that __runs__ whole Oracle
```
docker run orisi/zenoracles
```
* There must be an __oneliner__ to __fetch__ the newest image
```
docker pull orisi/zenoracles
```
* There must be a way to easily __update core Orisi code__ without interacting/logging into Orisi node
```
docker restart orisi/zenoracles
```

* There must be an easy way to fastly __build__ Orisi docker image __from source__
```
git clone git@github.com:orisi/zenoracles.git
cd zenoracles
docker build -t zenoracles .
```

* There must be a way to __deploy__ and test new code fast in __multiple scenarios and enviroments__



![ScreenShot](http://pixabay.com/static/uploads/photo/2014/04/05/11/32/stone-316225_640.jpg)

## Installation process

### Linux

If you're platform is Linux that probably means you can use docker natively:

##### Ubuntu - https://docs.docker.com/installation/ubuntulinux/
##### RedHat - https://docs.docker.com/installation/rhel/

If you have docker installed alraedy you can go straight to[Installing Orisi Docker Image](https://github.com/orisi/zenoracles/blob/master/README.md#installing-orisi-docker-image)


### Install Boot2Docker (for MacOSX and Windows users)

If you want to test zenoracles on a non-linux machine you're going to need to run a host for docker - a tiny smart virtual machine that can handle dockers, eats only 27mb of your RAM, and it's super fast.


Install process is very easy. It's just click and install.

#### Windows

https://github.com/boot2docker/windows-installer/releases

#### MacOSX

https://github.com/boot2docker/osx-installer/releases


After installing and opening Terminal window:

```
boot2docker init
boot2docker start
boot2docker ssh
```

You have succesfully logged into docker-host machine.

--



## Installing Orisi Docker Image


So you have Docker installed. Now the simple and fastest way to have an oracle up and running is to fetch Orisi image and run it.

```
docker pull orisi/zenoracles
```
This command will fetch an image of the pre-build docker container for Orisi. 

## Running Orisi

```
docker run orisi/zenoracles
```

## Building Orisi Docker Image from source

If you want to have everything installed from scratch you can just download the Dockerfile from the source:
```
git clone https://github.com/orisi/zenoracles.git
cd zenoracles
docker build -t zenoracle .
```

>Whole process should take around 20 minutes. Your mileage may vary.

## Running Orisi Oracles on Google Compute Engine

https://developers.google.com/compute/docs/containers/container_vms

It's very easy to run multiple Orisi nodes at the same time, or even a whole test set of Oracles and Clients using Google Compute engine because it supports special yaml files that allows you to create containers upon instance creation using "--metadata-from-file google-container-manifest=containers.yaml" parameter (it's a parameter to a gcloud command).



```
gcloud compute instances create orisi1 --image projects/google-containers/global/images/container-vm-v20140522 --metadata-from-file google-container-manifest=containers.yaml --zone europe-west1-b --machine-type n1-standard-1 --tags=http-server

```

## Running Orisi Oracles on AWS

Just run docker host optimized image, and from this point - the process is the same as described in this document.

https://docs.docker.com/installation/amazon/

## Updating your Orisi containers

```
docker pull 83tb/zenoracles
```

After getting the new image, restart the container. This will fetch every change in the docker container itself. But sometimes the container code will remain the same, you need "orisi code" updating mechanism.

This can be implemented easily in the Dockerfile (RUN command)
Thanks to this trick you're going to ONLY need to send "restart signal" to your containers.


![ScreenShot](http://upload.wikimedia.org/wikipedia/commons/b/b8/FullMeshNetwork.svg)




## Docker vs Full VM

So let's say you have a container image that is 1GB in size. If you wanted to use a Full VM, you would need to have 1GB times x number of VMs you want. With LXC and AuFS you can share the bulk of the 1.366 GB and if you have 1000 containers you still might only have a little over 1GB of space for the containers OS, assuming they are all running the same OS image.







