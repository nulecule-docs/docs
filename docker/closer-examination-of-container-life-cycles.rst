.. _docker-closer-examination-of-container-life-cycles:

====================================================
A Closer Examination of Docker Container Life-Cycles
====================================================

In :ref:`getting-started-example-explore-docker-container`, we've
started to explore a Docker container, but there is more to it.

To show that Docker nurtures your likely desire to communicate with
other systems and containers, let's look for an IP address:

.. parsed-literal::

    $ :command:`docker run fedora:20 ip a sh`
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    2324: eth0\@if2325: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:ac:11:00:78 brd ff:ff:ff:ff:ff:ff
        inet **172.17.0.120/16** scope global eth0
           valid_lft forever preferred_lft forever
        inet6 fe80::42:acff:fe11:78/64 scope link tentative 
           valid_lft forever preferred_lft forever

However, each of the commands we've been running so far create very,
very short-lived containers. 

SO far, we have created three separate containers, each of which has
only lived for as long as it has taken to complete the command issued.

The following few commands should bring this point home, by showing
that each time you execute a command the result is different.

.. parsed-literal::

    $ :command:`docker run fedora:20 ip a sh`
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    2326: eth0\@if2327: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
        link/ether 02:42:ac:11:00:79 brd ff:ff:ff:ff:ff:ff
        inet **172.17.0.121/16** scope global eth0
           valid_lft forever preferred_lft forever
        inet6 fe80::42:acff:fe11:79/64 scope link tentative 
           valid_lft forever preferred_lft forever
    $ :command:`docker run fedora:20 hostname`
    f26753e5ce33
    $ :command:`docker run fedora:20 hostname`
    ac6acaa8a502

However, if you where to execute :command:`rpm -qv fedora-release`
repetitively, there would not be a difference in the output since the
version of the package installed comes from the image, and as such is
the same for all containers spawned using that image.

.. parsed-literal::

    $ :command:`docker ps`
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

The :command:`docker ps` command shows us we have no running
containers. We do have containers that have run in the past, but they
have all exited:

.. parsed-literal::

    $ :command:`docker ps -a`
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
    ac6acaa8a502        fedora:20           "hostname"               12 minutes ago      Exited (0) 12 minutes ago                       suspicious_banach6
    f26753e5ce33        fedora:20           "hostname"               12 minutes ago      Exited (0) 12 minutes ago                       cocky_stallman
    962dc9d60f46        fedora:20           "ip a sh"                14 minutes ago      Exited (0) 14 minutes ago                       stupefied_einstein
    ca3a0655fc26        fedora:20           "ip a sh"                14 minutes ago      Exited (0) 14 minutes ago                       fervent_visvesvaraya
    e4d5fa15f371        fedora:20           "uname -a"               14 minutes ago      Exited (0) 14 minutes ago                       sick_sammet
    f4698e7ab40d        fedora:20           "rpm -qv fedora-relea"   14 minutes ago      Exited (0) 14 minutes ago                       stoic_feynman

If we wanted, we could start the containers again:

.. parsed-literal::

    $ :command:`docker start ac6acaa8a502`
    ac6acaa8a502
    $ :command:`docker ps -a`
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
    ac6acaa8a502        fedora:20           "hostname"               20 minutes ago      Exited (0) 5 seconds ago                        suspicious_banach6

It's not clear whether or not this executed the command we had
issued before was executed again.

:command:`docker start` by default does not attach stdout/stderr, so
let's attach it:

.. parsed-literal::

    $ :command:`docker start -a ac6acaa8a502`
    ac6acaa8a502

Still not clear. :command:`docker start` echoes, like in many other
sub-commands, the ID or name of the container.

.. parsed-literal::

    $ :command:`docker start suspicious_banach6`
    suspicious_banach6
    $ :command:`docker start -a suspicious_banach6`
    ac6acaa8a502


