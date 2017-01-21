# Start with Ubuntu16.04 image
FROM ubuntu:16.04
MAINTAINER Julien Guillaumin <julien.guillaumin@telecom-bretagne.eu>

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
	python \
        python3-dev \
        rsync \
        software-properties-common \
        unzip \
        libgtk2.0-0 \
        git \
	tcl-dev \
	tk-dev \
	nano \	
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install conda to manage python virtual env 
ADD https://repo.continuum.io/miniconda/Miniconda3-4.2.12-Linux-x86_64.sh tmp/Miniconda3-4.2.12-Linux-x86_64.sh
RUN bash tmp/Miniconda3-4.2.12-Linux-x86_64.sh -b
ENV PATH $PATH:/root/miniconda3/bin/

COPY environment.yml .
RUN conda env create -f environment.yml

# Cleanup tarballs and downloaded package files
RUN conda clean -tp -y

# Workdir
RUN mkdir /src
WORKDIR "/src"


COPY run.sh /
RUN chmod +x /run.sh
ENTRYPOINT ["/run.sh"]
