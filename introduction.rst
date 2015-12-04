============
Introduction
============

Why? What?


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
