This is a fork from randomdude/gcc-cross-x86_64-elf that contains the update dependencies to build an x86_64-elf-gcc toolchain. 
Here you can find the docker repo: https://hub.docker.com/r/maxbalej/gcc-cross-x86_64-elf-lt

```
FROM maxbalej/gcc-cross-x86_64-elf-lt:latest

RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get install -y grub-common

COPY ./ /root/

WORKDIR /root/
ENTRYPOINT build.sh # which invokes gcc/make for your own code
``

There's a docker image on the docker hub, so if you use that as a base, there's no need to build it yourself.

> docker pull maxbalej/gcc-cross-x86_64-elf-lt


