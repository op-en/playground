# Op-En Playground on Raspberry Pi

The Open Energy playground is also available for Raspberry Pi.

The instructions to getting started in almost the same as in the [main README](https://github.com/op-en/playground), except you have to use the docker-compose.yml file in this folder (rpi) instead.

## Installing Docker on the Pi

1. Follow the guide on http://blog.hypriot.com/getting-started-with-docker-on-your-arm-device/

2. When docker is up and running and you are connected to the pi via ssh:

Clone the Open Energy Playground and run the compose script in the rpi folder:
```
git clone https://github.com/op-en/playground.git
cd playground/rpi
docker-compose up -d
```
Thats it!

When the compose script is finished, the playground is ready.

## Accessing the Playground

On linux, the docker containers map to localhost.

## Containers in the Playground

See the contents of [rpi/docker-compose.yml](https://github.com/op-en/playground/blob/master/rpi/docker-compose.yml)
