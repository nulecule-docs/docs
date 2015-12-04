FROM centos:centos7

RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

RUN yum -y install httpd && yum clean all

CMD [ "/usr/sbin/httpd", "-DFOREGROUND" ]
