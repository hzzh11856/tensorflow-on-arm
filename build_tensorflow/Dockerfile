FROM debian:stretch

RUN dpkg --add-architecture armhf && dpkg --add-architecture arm64 \
    && apt-get update && apt-get install -y \
        openjdk-8-jdk automake autoconf \
        curl zip unzip libtool swig zlib1g-dev pkg-config git g++ wget xz-utils \
        python-numpy python-pip python-mock \
        libpython3-dev libpython3-all-dev \
        libpython3-dev:armhf libpython3-all-dev:armhf \
        libpython3-dev:arm64 libpython3-all-dev:arm64

RUN update-alternatives --install /usr/bin/python python /usr/bin/python2 100 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3 150

RUN echo "deb http://httpredir.debian.org/debian/ jessie main contrib non-free" > /etc/apt/sources.list.d/jessie.list \
    && apt-get update && apt-get install -y libpng12-dev \
    && rm -f /etc/apt/sources.list.d/jessie.list \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install -U --user keras_applications==1.0.5 --no-deps \
    && pip3 install -U --user keras_preprocessing==1.0.3 --no-deps \
    && ldconfig

WORKDIR /root
RUN git clone https://github.com/hzzh11856/tensorflow-on-arm/

WORKDIR /root/tensorflow-on-arm/build_tensorflow/
RUN git checkout v1.12.0
CMD ["/bin/bash"]
