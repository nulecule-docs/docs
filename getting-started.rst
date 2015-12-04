.. _getting-started:

===============
Getting Started
===============

We'll get started with the :ref:`docker-quick-installation-guide`, the
minimal prerequisite to generate something to show for.

Next, create a place to work. This is usually a directory hierarchy in
your home directory, that you can put under revision control.

The few walk-through examples in this chapter illustrate the some uses
of Docker containers and images in annotated fashion.

.. _getting-started-example-explore-docker-container:

Example #1: Explore a Docker Container
======================================

For this first exercise, we're going to run a few Fedora 20 Docker
containers and poke at them.

First, let's see what the version is of the **fedora-release** package
installed in the official Fedora 20 image:

.. parsed-literal::

    $ :command:`docker run fedora:20 rpm -qv fedora-release`
    fedora-release-20-4.noarch

Success!

.. seealso::

    *   :ref:`docker-closer-examination-of-container-life-cycles`

Example #2: Fedora 20 Welcome Page
==================================

Create a directory ``example-2/``, with a file named ``Dockerfile``
containing the following:

.. literalinclude:: docker/examples/fedora-20-welcome-page/Dockerfile
    :linenos:

A line-by-line explanation of the instructions for the image:

**#1**

    Create the new image from the `docker.io/library/fedora:20`_ base
    image.

**#3**

    Runs the command specified inside the image.

    A container is spawned based on the previous version of the image,
    which in this case specifically is the base image downloaded from
    the `public Docker Hub`_.

    The command that runs imports the GPG key used to sign the packages
    for Fedora 20 in to the RPM database of trusted keys, to prevent
    warnings [#]_.

    .. NOTE::

        Arguably, this command should be a part of the
        `docker.io/library/fedora:20`_ base image.

**#5**

    Install the **httpd** software package using YUM.

    .. NOTE::

        For Docker images to remain slim, clean out
        :file:`/var/cache/yum/` which will contain repository metadata
        even after the installation of the package has been
        successfully completed.

**#7**

    Using the ``CMD`` directive, specify that the command specified in
    the JSON-formatted array (i.e. "list") should be run.

    .. todo:: why not systemd?


    .. todo:: also, ``ENTRYPOINT``

Build the Docker image:

.. parsed-literal::

    $ :command:`docker build -t nulecule-docs/example-2 example-2/.`

Run the Docker image:

.. parsed-literal::

    $ :command:`docker run -it -p 172.17.42.1:80:80 nulecule-docs/example-2`

Now, visit http://172.17.42.1/

.. TODO:: Explain the build command
.. TODO:: Explain the run command
.. TODO:: Stop the container (Ctrl-C)

Example #3: CentOS 7 Welcome Page
=================================

Create a directory ``example-3/`` and put a file named ``Dockerfile``
in it, containing the following:

.. literalinclude:: docker/examples/centos-7-welcome-page/Dockerfile
    :linenos:

.. literalinclude:: docker/examples/centos-7-welcome-page/Dockerfile
    :linenos:
    :diff: docker/examples/fedora-20-welcome-page/Dockerfile

Build the Docker image:

.. parsed-literal::

    $ :command:`docker build -t nulecule-docs/example-3 example-3/.`

Run the Docker image:

.. parsed-literal::

    $ :command:`docker run -it -p 172.17.42.1:80:80 nulecule-docs/example-3`

Now, visit http://172.17.42.1/

TODO: “Notice the difference?”

.. rubric:: Footnotes

.. [#]  :ref:`docker-example-outputs-fedora-20-without-gpg-key-import`
