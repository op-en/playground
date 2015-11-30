# Table of Contents

<!-- TOC depth:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Table of Contents](#table-of-contents)
- [Open Energy Playground](#open-energy-playground)
	- [Introduction](#introduction)
	- [The Playground and Docker](#the-playground-and-docker)
	- [Installing the playground](#installing-the-playground)
	- [Accessing the Playground](#accessing-the-playground)
	- [Containers in the Playground](#containers-in-the-playground)
- [On Docker containers](#on-docker-containers)
	- [External Volumes](#external-volumes)
	- [Running containers and logging](#running-containers-and-logging)
	- [Port mapping](#port-mapping)
	- [Getting inside a container](#getting-inside-a-container)

<!-- /TOC -->

# Open Energy Playground

## Introduction

Open Energy Playground is a research project aiming to make it easier and faster to prototype smart energy services.

Energy data is collected and measured from sites such as offices, homes, construction sites and museums.
This data is then analyzed, stored and processed with tools from the toolbox to result in mockups, tutorials, research material and concept services.
Data will be made available through open source when the project is finished.

## The Playground and Docker

The processing platform (or playground) is built on number of Docker containers.
But, what is Docker?

"Docker containers wrap up a piece of software in a complete filesystem that contains everything it needs to run: code, runtime, system tools, system libraries – anything you can install on a server. This guarantees that it will always run the same, regardless of the environment it is running in."

\- [Docker](https://www.docker.com)

To get started, go through the first step in the Docker getting started guide ([Mac](http://docs.docker.com/mac/step_one/), [Windows](http://docs.docker.com/windows/step_one/) or [Linux](http://docs.docker.com/linux/step_one/)). Then come back here!


## Installing the playground
Clone the Open Energy Playground:
```
git clone https://github.com/op-en/playground.git
```
This project contains only a Docker Compose file that specifies what programs to download, and how to run them on your computer. To download, install and startup all these programs, go into the project folder and run docker-compose, like so:
```
cd playground/
docker-compose up -d
```
Thats it!

When the compose script is finished, the playground is ready.

## Accessing the Playground

First you have to find the public ip of the docker-machine that is running the container.
You can find this in two ways:

1\. When you start up the docker environment, it outputs the ip, like this:

```
                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.100
```

2\. If the machine is already running, you can get the ip by running

```
docker-machine ip default
```

## Containers in the Playground

The playground currently contains 6 containers.

- [InfluxDB](https://influxdb.com/), a database.
- [Grafana](http://grafana.org/), a visualizing tool.
- [Mosquitto](http://mosquitto.org/), a broker relaying [MQTT](http://mqtt.org/) messages.
- [node-RED](http://nodered.org/), a tool for wiring everything together.
- [App Server](https://github.com/op-en/app-server), a bridge from MQTT to websockets.
- [nginx](http://nginx.org/), a web server hosting your custom content.


# On Docker containers

There is a lot to know and learn about Docker containers. Some of the most important aspects when it comes to the playground is discussed here.

## External Volumes

It is very important to understand the ephemeral nature of containers. This means that data created and stored within the container can disappear if the container restarts or is stopped.

For example, if we do not specify where the flows should be stored when running the node-RED container, they will be stored on the container itself. And the next time you restart the container, all you work will be LOST! Tragic!

To avoid this, the compose script (by default) maps the folder in the container that stores the flows to another folder on the host system. In the compose file, this is specified as the node-red folder within this project.

With this mapping in place, the flows are persistent beyond a restart.

## Running containers and logging

You can see what containers are running with:

    docker ps

And the images available with:
```
docker images
```

## Port mapping

If deployed with this compose script, the ports from the containers are automatically mapped to the host.

## Getting inside a container

If you want to run something custom inside an image, you can run:
```
docker exec -t -i [docker image] /bin/bash
```
