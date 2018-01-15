FROM kalilinux/kali-linux-docker
MAINTAINER Yanis Pavlidis <yanis@pavlidis.email>

WORKDIR /data

ENV DEBIAN_FRONTEND noninteractive

RUN set -x \
    && apt-get -yqq update \
    && apt-get install -y \
   	kali-linux-full \
   	pciutils \
   	&& apt-get autoremove -y \
    && apt-get clean

CMD ["bash"]