============
Introduction
============

Docker provides easy to use, light-weight containers that run
processes mostly isolated from the host operating system.

Pieces of the collection of underlying technology have been around for
quite a while, and probably sound more familiar as virtual private
servers (VPS), jails, Linux Containers (LXC) or chroots.

Unlike virtual machines, containers do not require a separate operating
system instance to run, and instead relies on Linux kernel support for
namespaces and cgroups, such that the processes that run within a
container have an isolated view of the operating system.

Docker specifically facilitates the creation and distribution of
images, the deployment of containers based on these images, as well as
various networking and storage aspects.

The images distributed result in running relatively short-lived
containers, bringing about a new dimension to system life-cycle
management, and great opportunities for fast delivery and deployment of
turn-key solutions.

What does this mean?
====================

A piece of software can be developed with either of two completely
separate mindsets driving the development team;

#.  Ensure that the functionality set out at the beginning of the
    development project functions on a pre-defined target platform.

#.  Work to ensure the developer's excel the naughtiest expectations
    for the software by whatever means necessary.

While there is also a center between this left and right, and shades of
grey between white and black, there's little that sets a software
development project up for failure better.

The former development strategy is a so-called waterfall metholodogy.

There's a boundary between a developer's workstation and a server
platform.

.. TODO::

    Ramble on a bit about the various aspects in which this has effect;

    *   Micro-services ("lab mice") rather than pets or cattle, w/;

        *   scalability per unit in role,

        *   looser dependencies,

        *   roll-over deployment methodologies.

    *   "Works on my system" syndrome

    *   Agility and speed of delivery, including:

        *   Delivery to retrospective in agile development methodology
            Scrum.

        *   Continuous Integration.

.. seealso::

    *   :ref:`docker-quick-installation-guide`

Continue with our :ref:`getting-started` chapter.
