FROM debian:bullseye-slim

# Install Whisper
WORKDIR /usr/src
ARG WYOMING_WHISPER_VERSION='2.4.0'

RUN \
  apt-get update &&\
  apt-get install -y --no-install-recommends \
  build-essential wget python3 python3-dev python3-pip python3-setuptools python3-wheel &&\
  pip3 install ctranslate2==4.4.0 &&\
  pip3 install --no-cache-dir --extra-index-url https://www.piwheels.org/simple \
  "wyoming-faster-whisper @ https://github.com/rhasspy/wyoming-faster-whisper/archive/refs/tags/v${WYOMING_WHISPER_VERSION}.tar.gz" &&\
  wget https://developer.download.nvidia.com/compute/cuda/repos/debian12/x86_64/cuda-keyring_1.1-1_all.deb &&\
  wget https://developer.download.nvidia.com/compute/cuda/repos/debian11/x86_64/libcudnn8_8.9.7.29-1+cuda12.2_amd64.deb &&\
  dpkg -i cuda-keyring_1.1-1_all.deb &&\
  apt-get update &&\
  apt-get install -y --no-install-recommends cudnn libcublas-12-6 &&\
  dpkg -i libcudnn8_8.9.7.29-1+cuda12.2_amd64.deb &&\
  rm -f cuda-keyring_1.1-1_all.deb libcudnn8_8.9.7.29-1+cuda12.2_amd64.deb &&\
  apt-get purge -y --auto-remove build-essential python3-dev &&\
  apt-get clean &&\
  rm -Rf /var/lib/apt/lists/*

WORKDIR /
COPY entrypoint.sh /
EXPOSE 10300
ENTRYPOINT ["bash", "/entrypoint.sh"]
