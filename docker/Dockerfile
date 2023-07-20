FROM --platform=linux/amd64 python:3.11.4

RUN mkdir -p /src
WORKDIR /src

ENV PIP_VERSION=23.1.2
ENV POETRY_VERSION=1.5.1
ENV POETRY_HOME=/opt/poetry
RUN python3 -m venv ${POETRY_HOME}

RUN ${POETRY_HOME}/bin/pip install --upgrade pip==${PIP_VERSION}
RUN ${POETRY_HOME}/bin/pip install poetry==${POETRY_VERSION}
ENV PATH="$PATH:${POETRY_HOME}/bin"

RUN apt-get update && apt-get -y install patchelf pigz
RUN pip3 install pyinstaller==5.12.0 staticx==0.13.9

ENV POETRY_CACHE_DIR=/src/build_output/pypoetry

RUN mkdir -p /src
WORKDIR /src
