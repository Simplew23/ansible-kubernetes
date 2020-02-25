FROM centos:7

COPY resources/etc/yum.repos.d/* /etc/yum.repos.d/

RUN yum -y update

RUN yum makecache

RUN yum install -y kamailio kamailio-debuginfo kamailio-utils kamailio-sctp kamailio-json gdb

WORKDIR /etc/kamailio/

EXPOSE 5060/udp

CMD ["/usr/sbin/kamailio", "-m 1024", "-M 64", "-D"] 

COPY resources/etc/kamailio/* /etc/kamailio/
