FROM debian:jessie

RUN echo "nameserver 8.8.8.8" > /etc/resolv.conf

RUN sed --in-place 's@main@main contrib non-free@g' /etc/apt/sources.list

RUN apt-get update && apt-get -y install \
    git-core \
    curl \
    wget \
    make \
    nano \
    htop \
    libssl-dev \
    libnl-genl-3-dev \
    pkg-config \
    build-essential \
    pyrit \
    nvidia-cuda-toolkit \
    nvidia-opencl-icd \
    python2.7-dev \
    python2.7-libpcap \
    libpcap-dev \
    p7zip-full

#    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /usr/src/app/password_lists
RUN mkdir -p /usr/src/app/captures

RUN cd /usr/src \
    && wget https://pyrit.googlecode.com/files/cpyrit-cuda-0.4.0.tar.gz \
    && tar -xzf cpyrit-cuda-0.4.0.tar.gz \
    && cd cpyrit-cuda-0.4.0 \
    && python setup.py build \
    && python setup.py install

RUN cd /usr/src \
    && wget http://hashcat.net/files/cudaHashcat-1.33.7z \
    && 7z x cudaHashcat-1.33.7z \
    && ln -s /usr/src/cudaHashcat-1.33/cudaHashcat64.bin /usr/local/bin/cudaHashcat64.bin

WORKDIR /usr/src/app

# Beanstalk runs non interactive mode, so CMD needs to block
CMD sleep infinity