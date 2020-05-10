FROM continuumio/anaconda3:2020.02

USER root

ENV UBUNTU_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8 \
    NOTEBOOK_DIR=/home/JupiterNotebook \
    NOTEBOOK_IP=0.0.0.0 \
    NOTEBOOK_PORT=8888

RUN pip install watermark

RUN mkdir ${NOTEBOOK_DIR}

WORKDIR ${NOTEBOOK_DIR}

VOLUME ["${NOTEBOOK_DIR}"]

CMD jupyter notebook \
    --notebook-dir=${NOTEBOOK_DIR} \
    --ip=${NOTEBOOK_IP} \
    --port=${NOTEBOOK_PORT} \
    --NotebookApp.token='' \
    --no-browser \
    --allow-root