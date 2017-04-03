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

When I do this:
```
docker run -v /tmp/outside:/tmp/inside -it ubuntu
]0;root@5ff854488c54: /root@5ff854488c54:/# mount
]0;root@5ff854488c54: /root@5ff854488c54:/# mount
... lots of entries ...
osxfs on /tmp/inside type fuse.osxfs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,allow_other,max_read=1048576)
... lots of entries ...
]0;root@5ff854488c54: /root@5ff854488c54:/# 
```

I see an 'osxfs' file system mounted on /tmp/inside.

When I run 'mount' from within the Dockerfile invoked by docker-compose - there are no osxfs file systems mounted anywhere. WTH?
