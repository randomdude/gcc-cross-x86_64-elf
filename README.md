This code was shamelessly taken from https://github.com/beevik/docker - I've changed only about two words in the source. I've changed some deps to come over via HTTPS instead of FTP but that's about it. Thanks to Brett Vickers for the original work.

Anyway, this will build an x86_64-elf-gcc toolchain. I use it to build code which runs without an OS present (ie, GRUB loads it).

The resulting image is of an Debian stretch image with the built toolchain installed and ready to go.

To use it, you can simply build and run this container, and then 'docker exec gcc ...' to compile.
Or, you can build your project in a container based on this one. For an example, see the 'btstestbench' project, which does this:
```
FROM randomdude/gcc-cross-x86_64-elf

RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get install -y grub-common

COPY ./ /root/

WORKDIR /root/
ENTRYPOINT build.sh # which invokes gcc/make for your own code
``

There's a docker image on the docker hub, so if you use that as a base, there's no need to build it yourself.

> docker pull randomdude/gcc-cross-x86_64-elf


