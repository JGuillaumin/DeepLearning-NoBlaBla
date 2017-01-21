FROM nvidia/cuda:8.0-cudnn5-devel

MAINTAINER Julien Guillaumin <julien.guillaumin@telecom-bretagne.eu>

# Pick up some TF dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python \
        python-dev \
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

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

RUN pip --no-cache-dir install \
        jupyter \
        matplotlib \
        numpy \
        scipy \
        sklearn \
        Pillow \
	scikit-learn \
   	scikit-image \
	scipy \
	h5py \
	pandas


# Install TensorFlow GPU version.
RUN pip --no-cache-dir install https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp27-none-linux_x86_64.whl

RUN pip install keras quiver

# Workdir
RUN mkdir /src
WORKDIR "/src"

COPY run-gpu.sh /
RUN chmod +x /run-gpu.sh
ENTRYPOINT ["/run-gpu.sh"]

