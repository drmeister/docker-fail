#  Problem with docker-compose

Why can't I mount the host directory /tmp/outside within the container at /tmp/inside?????

```
docker-compose build build
```

I want it to copy a file into /tmp/outside on the host system.
It refuses to comply.

I can however do this:
```
Dock$ docker run -it -v /tmp/outside:/tmp/inside ubuntu
]0;root@c1b8929d0e28: /root@c1b8929d0e28:/# touch /tmp/inside/a
touch /tmp/inside/a
]0;root@c1b8929d0e28: /root@c1b8929d0e28:/# exit
meister@MacBook-Pro-2 Dock$ ls /tmp/outside
a
meister@MacBook-Pro-2 Dock$
```

It's madness I tell you - madness!


----

**The Method behind the Madness**


The reason this didn't work before is that you can't mount a host volume during the build stage. Your attempts to create a file in `/tmp/inside` were successful during the build, but that entire directory became unavailable at the time the `command` was executed, because its place in the filesystem hierarchy was overridden with the volume mount!

The committed changes enable the following with only `git` and `docker-compose` installed:

    git clone https://github.com/drmeister/docker-fail.git docker-success
    cd docker-success
    docker-compose run build
    cat /tmp/outside/dockertest.txt


When `docker build ...` is run, the docker client uploads _only the context directory_ (the argument passed to `docker build`) to the docker server. So for the purposes of all `RUN` directives in the `Dockerfile`, _only_ stuff within the build context directory is accessible. Recall that there is no `-v` parameter when using `docker build`. Basically, `docker-compose` just sites on top of the regular docker client, as a workflow tool, so it can't do anything you can't do yourself with manual steps.

 Now, when you use `docker run`, or when `docker-compose` does the same thing, you _can_ mount a volume. So in short, the host volume _is_ available when the `command` specified in the `docker-compose` file is run, but not when any of the `RUN` directives are processed during the `docker build...`.
