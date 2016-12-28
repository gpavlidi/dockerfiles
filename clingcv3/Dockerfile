FROM gpavlidi/cling
MAINTAINER Yanis Pavlidis <yanis@pavlidis.email>

RUN echo "deb http://httpredir.debian.org/debian experimental main" | tee -a /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get -t experimental install -y libopencv-dev --no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV LANG en-US

ENTRYPOINT [ "cling" ]