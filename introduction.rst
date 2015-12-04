============
Introduction
============

Docker provides easy to use, light-weight containers that run
processes mostly isolated from the host operating system.

Pieces of the collection of underlying technology have been around for
quite a while, and probably sound more familiar as virtual private
servers (VPS), jails, Linux Containers (LXC) or chroots.

Unlike virtual machines, Docker does not require a separate operating
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

.. todo:: create a place to work

Example #1: Fedora 20 Welcome Page
==================================

Create a directory ``example-1/``, with a file named ``Dockerfile`` containing the following:

.. code-block:: none
    :linenos:

    FROM fedora:20

    RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-20-x86_64

    RUN yum -y install httpd && \
          yum clean all

    EXPOSE 80

    CMD [ "/usr/sbin/httpd", "-DFOREGROUND" ]

Build the Docker image:

.. parsed-literal::

    $ :command:`docker build -t nulecule-docs/example-1 example-1/.`

Run the Docker image:

.. parsed-literal::

    $ :command:`docker run -it -p 172.17.42.1:80:80 nulecule-docs/example-1`

Now, visit http://172.17.42.1/

.. TODO:: Explain line-by-line for the Docker file.
.. TODO:: Explain the build command
.. TODO:: Explain the run command
.. TODO:: Stop the container (Ctrl-C)

Example #2: CentOS 7 Welcome Page
=================================

Example #2: Do the same but based on CentOS 7. Create a directory example-2/ and put a file named Dockerfile in it, containing the following:

.. code-block:: none
    :linenos:

    FROM centos:centos7

    RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    RUN yum -y install httpd && yum clean all

    EXPOSE 80

    CMD [ "/usr/sbin/httpd", "-DFOREGROUND" ]

Build the Docker image:

.. parsed-literal::

    $ :command:`docker build -t nulecule-docs/example-2 example-2/.`

Run the Docker image:

.. parsed-literal::

    $ :command:`docker run -it -p 172.17.42.1:80:80 nulecule-docs/example-2`

Now, visit http://172.17.42.1/

TODO: “Notice the difference?”
