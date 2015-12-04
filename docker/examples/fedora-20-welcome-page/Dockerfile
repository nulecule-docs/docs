FROM docker.io/library/fedora:20

RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-fedora-20-x86_64

RUN yum -y install httpd && yum clean all

CMD [ "/usr/sbin/httpd", "-DFOREGROUND" ]
