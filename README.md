Your command
     |
     | ./container run /bin/sh
     v
+----------------------+
|       Go Runtime     |
|                      |
|       run()          |
+----------+-----------+
           |
           | fork/exec
           | + Linux Namespaces
           v
+----------------------+
|      child()         |
|                      |
|  UTS Namespace       | ---> hostname = container
|  PID Namespace       | ---> isolated process IDs
|  Mount Namespace     | ---> isolated mounts
|                      |
|  Chroot              | ---> /tmp/alpine-rootfs = /
|                      |
|  Mount /proc         | ---> process filesystem
+----------+-----------+
           |
           v
     /bin/sh
     /bin/ps
     /bin/...
