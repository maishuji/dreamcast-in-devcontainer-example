# Project : Dreamcast development with devcontainer example.

## Introduction

This example comes from the official repository of KOS (https://github.com/KallistiOS/KallistiOS). It has been adapted to work with CMake and devcontainer.
It aims to illustrate how to setup a devcontainer for dreamcast programming.

## Docker image

The docker image used in thedevcontainer comes from https://hub.docker.com/repository/docker/maishuji/dc-kos-image.
The docker image definition is available at https://github.com/maishuji/dreamcast-kos-docker

## Dev container

In case you can't push change to your repository while inside the container, 
It is probable that you need to add your local SSH keys to the agent
```ssh-add $HOME/.ssh/<your ssh key>```
Please check this link: https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials