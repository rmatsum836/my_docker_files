FROM continuumio/miniconda3:4.7.12-alpine

#ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH
ENV MOSDEF https://github.com/mosdef-hub
ENV PY_VER 3.7

# Add files
ADD . / /tmp/

#USER anaconda
USER root

# Set workdir
WORKDIR /tmp

RUN apk add --no-cache git

RUN conda config --set always_yes yes --set changeps1 no \
    && conda config --add channels omnia \
    && conda config --add channels mosdef \
    && conda config --add channels conda-forge \
    && conda update --all -y \
    && conda install -y python=3 conda conda-build pip mbuild foyer \
    && git clone https://github.com/rmatsum836/Pore-Builder.git \
    && cd Pore-Builder \
    && pip install -e . \
    && cd .. \ 
    && conda clean -ya

CMD [ "python", "./initialize.py" ]
