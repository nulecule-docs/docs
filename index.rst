=================
The Nulecule Book
=================

When we say a service runs "in the cloud", we mean to indicate that the
the service provided is *elastic* -- scaling up and down as demand
requires.

The usual line of thinking is to build an image, and spin up many
instances of an application using that image as the basis.

Very few services, however, are provided with the help of just one
single application, and even fewer come off the shelf naturally able to
scale up and down by themselves and without assistance.

This has spawned a need for run-time orchestration. A frontend
web-server application can certainly not maintain session-validity
databases on the instance's local filesystem, because that database is
not available to other instances of the same frontend web-server
application. Thus, the instance needs to learn where to store its
session-validity database so that it is available to all instances.

.. toctree::
    :maxdepth: 1

    introduction
    getting-started

.. toctree::
    :glob:
    :hidden:

    docker/closer-examination-of-container-life-cycles
    docker/example-outputs/*
    docker/quick-installation-guide
