FROM ubuntu:16.04

MAINTAINER sh-tatsuno
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

RUN apt-get -y install git \
                       cmake \
                       make \
                       gcc \ 
                       build-essential \
                       libssl-dev \
                       zlib1g-dev \ 
                       libbz2-dev \
                       libreadline-dev \
                       libsqlite3-dev \
                       curl \
                       mysql-client \
                       python-dev \
                       python-pip \
                       wget \
                       fonts-takao-gothic \
                       vim \
                       unzip 

RUN curl -L https://github.com/krallin/tini/releases/download/v0.6.0/tini > tini && \
    echo "d5ed732199c36a1189320e6c4859f0169e950692f451c03e7854243b95f4234b *tini" | sha256sum -c - && \
    mv tini /usr/local/bin/tini && \
    chmod +x /usr/local/bin/tini

# language setting
RUN apt-get install -y language-pack-ja 
ENV LANG ja_JP.UTF-8

# install pyenv
RUN git config --global url.https://github.com/.insteadOf git://github.com/
RUN git clone git://github.com/yyuu/pyenv.git /root/.pyenv
RUN git clone https://github.com/yyuu/pyenv-pip-rehash.git /root/.pyenv/plugins/pyenv-pip-rehash
ENV PYENV_ROOT /root/.pyenv
ENV PATH $PYENV_ROOT/bin:$PATH
RUN echo 'eval "$(pyenv init -)"' >> .bashrc


# install anaconda
ENV ANACONDA_VER 4.4.0
RUN pyenv install anaconda3-$ANACONDA_VER
RUN pyenv global anaconda3-$ANACONDA_VER
ENV PATH $PYENV_ROOT/versions/anaconda3-$ANACONDA_VER/bin:$PATH

RUN conda update -y conda
RUN pip install --upgrade pip

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

# install python module
RUN pip install --upgrade \
  apyori \
  networkx \
  boto3 \
  nose \
  psycopg2 \
  xgboost \
  SQLAlchemy \
  theano \
  bs4 \
  tqdm \
  simplejson \
  gensim \
  nimfa \
  selenium \
  pydot \
  pyparsing \
  graphviz \
  lightgbm 

# install pytorch 
RUN conda install -y pytorch torchvision -c soumith

# install MeCab
RUN apt-get -y install mecab mecab-ipadic-utf8 swig libmecab-dev mecab-ipadic
RUN pip install mecab-python3
RUN conda install libgcc

# install OpenCV
RUN conda install opencv

# install gcp
WORKDIR /
RUN apt-get install -qqy apt-transport-https lsb-release openssh-client && \
    pip install crcmod   && \
    export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb https://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" > /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update && \
    apt-get install -y google-cloud-sdk \
        google-cloud-sdk-app-engine-python 

RUN conda install anaconda setuptools=27.2.0
RUN pip install google-cloud-bigquery
RUN pip install pandas-gbq

# other libraries
RUN pip install \
  edward \
  wheel \
  tensorflow \
  keras 

# mysqlをpythonに導入
RUN apt-get -y install libmysqlclient-dev
RUN pip install mysqlclient

WORKDIR /notebooks

ENTRYPOINT ["tini", "--"]
CMD ["/bin/bash"]