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
