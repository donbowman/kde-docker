## kde-docker

This repository contains kde-docker, Ubuntu 16.04 + kde neon, using spice as display.

It may be useful with [spice-web-client](https://github.com/eyeos/spice-web-client) to
provide a web-based access to your kde desktop.

It explicitly disables compositing to get better perceived performance, but feel
free to re-enable and experiment.

Inspiration from [DockerSpiceXfce4](https://github.com/gauthierc/DockerSpiceXfce4)

### Base Docker Image

* [ubuntu:16.04](https://registry.hub.docker.com/_/ubuntu/)

### Installation

    docker build -t="donbowman/kde-docker" github.com/donbowman/kde-docker

### Usage

    docker run -p 5900:5900 donbowman/kde-docker

You may want a different ~/.config if you are running this on the same host you already
run kde. mkdir ~/.config-kde-docker and mount it.

If you local user is 'myusername' and your uid is '1000' and you want map your /home/myusername in Docker:

	docker run --name kde -p 5900:5900 -e SPICE_USER=myusername -e SPICE_UID=1000 -v /home/myusername:/home/myusername -e -v /home/myusername/.config-kde-docker:/home/myusername/.config SPICE_PASSWD="password" -e SPICE_LOCAL="en_CA.UTF-8" -e SPICE_RES="1920x1080" donbowman/kde-docker

A simple way to make a container which is 'you' is:

	docker run --name kde -p 5900:5900 -e SPICE_USER=$(whoami) -e SPICE_UID=$(id -u) -v $HOME:/home/$(whoami) -v $HOME/.config-kde-docker:$HOME/.config -e SPICE_PASSWD="password" -e SPICE_LOCAL="en_CA.UTF-8" -e SPICE_RES="1920x1080" donbowman/kde-docker

Connect via Spice client

        spicy -h localhost -p 5900

The default password is 'password'.

