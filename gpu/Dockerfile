FROM nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04

USER root

ENV UBUNTU_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    PATH=/opt/conda/bin:$PATH \
    NOTEBOOK_DIR=/home/JupiterNotebook \
    NOTEBOOK_IP=0.0.0.0 \
    NOTEBOOK_PORT=8888

RUN apt-get -y update -qq \
    && apt-get upgrade -y \
    &&  apt-get install -y wget bzip2 ca-certificates \
    git mercurial subversion

# Instalación de anaconda3:
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
    && ANACONDA_INSTALL_SCRIPT='Anaconda3-2020.02-Linux-x86_64.sh' \
    && wget --quiet https://repo.continuum.io/archive/$ANACONDA_INSTALL_SCRIPT -O ~/anaconda.sh \
    && /bin/bash ~/anaconda.sh -b -p /opt/conda \
    && rm ~/anaconda.sh \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip install watermark

RUN mkdir ${NOTEBOOK_DIR}

WORKDIR ${NOTEBOOK_DIR}

VOLUME ["${NOTEBOOK_DIR}"]

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]

CMD jupyter notebook \
    --notebook-dir=${NOTEBOOK_DIR} \
    --ip=${NOTEBOOK_IP} \
    --port=${NOTEBOOK_PORT} \
    --NotebookApp.token='' \
    --no-browser \
    --allow-root