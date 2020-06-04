# Dockerfile for building PyKaldi image from Ubuntu 16.04 image
FROM ubuntu:18.04

RUN sed -i 's|http://archive|http://us.archive|g' /etc/apt/sources.list
RUN DEBIAN_FRONTEND="noninteractive" apt-get update && apt-get -y install tzdata

# Install necessary system packages
RUN apt-get update \
    && apt-get install -y \
    python3 \
    python3-pip \
    python2.7 \
	python3.7-dev \
	python3.7 \
    autoconf \
    automake \
    cmake \
    curl \
    build-essential \
    g++ \
    git \
    graphviz \
    libatlas3-base \
    libtool \
    make \
    pkg-config \
    sox \
    subversion \
    unzip \
    wget \
    ninja-build \
    zlib1g-dev

# Install systems protobuf
RUN apt-get install -y libprotobuf-dev libprotobuf-c-dev protobuf-c-compiler protobuf-compiler

# Make python3.7 default
RUN ln -sf /usr/bin/python3.7 /usr/bin/python3 \
	&& ln -sf /usr/bin/python3 /usr/bin/python \
    && ln -sf /usr/bin/pip3 /usr/bin/pip
	
RUN python --version

# Install necessary Python packages
RUN pip install --upgrade pip \
    numpy \
    setuptools \
    pyparsing \
    jupyter \
    ninja

# Copy pykaldi directory into the container
#RUN git clone https://github.com/pykaldi/pykaldi.git /pykaldi
COPY . /pykaldi

# Install CLIF, Kaldi and PyKaldi
RUN cd /pykaldi/tools \
    && ./check_dependencies.sh \
    && ./install_clif.sh \
    && ./install_kaldi.sh \
    && cd .. \
    && python setup.py install
