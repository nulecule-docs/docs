.. _docker-quick-installation-guide:

===============================
Docker Quick Installation Guide
===============================

This quick installation guides assumes you are running a current Fedora
workstation, and you have no special requirements or ideas or other
such adventures in mind.

.. .. seealso::

    *   :ref:`docker-installation-guide`

Install, configure and run Docker:

#.  Install the **docker** package:

    .. parsed-literal::

        # :command:`dnf -y install docker`

#.  Add a *docker* group:

    .. parsed-literal::

        # :command:`groupadd -r docker`

#.  Add your user account to the *docker* group, for example ``jdoe``:

    .. parsed-literal::

        # :command:`gpasswd -a jdoe docker`

#.  Start the **docker** service and configure it to be started when
    the system reboots:

    .. parsed-literal::

        # :command:`systemctl start docker.service`
        # :command:`systemctl enable docker.service`

#.  Verify Docker works, and pull an image if you feel so inclined:

    .. parsed-literal::

        # :command:`docker ps -a`
        # :command:`docker images -a`
        # :command:`docker pull centos:centos7`

#.  Log out the ``jdoe`` user account completely to let the new group
    membership take effect.


