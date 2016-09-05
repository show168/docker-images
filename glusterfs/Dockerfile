FROM ubuntu:trusty

EXPOSE 24007
EXPOSE 24007/udp
EXPOSE 24008
EXPOSE 24008/udp
EXPOSE 49152

VOLUME ["/data/glusterfs"]

ENTRYPOINT ["/glusterfs/start.sh"]


RUN apt-get update -y

RUN apt-get install -y software-properties-common \
  && add-apt-repository -y ppa:gluster/glusterfs-3.8 && apt-get update \
  && apt-get install -y glusterfs-server


ADD ./*.sh /glusterfs/
RUN chmod +x /glusterfs/*.sh

EXPOSE 49153-59153


# Master only:
# CMD ["host1,host2,host3"]

RUN apt-get install -y openssh-server

RUN sed -ri 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN sed -ri 's/#Port 22/Port 2222/g' /etc/ssh/sshd_config
RUN mkdir -p /var/run/sshd && chmod 755 /var/run/sshd
RUN mkdir /root/.ssh && chmod -R g-rwx,o-rwx /root/.ssh

EXPOSE 2222
