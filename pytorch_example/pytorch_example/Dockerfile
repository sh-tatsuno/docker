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
                       curl \
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

# install pytorch
RUN conda install -y pytorch torchvision -c soumith

# install MeCab
RUN apt-get -y install mecab mecab-ipadic-utf8 swig libmecab-dev mecab-ipadic
RUN pip install mecab-python3

WORKDIR /notebooks

ENTRYPOINT ["tini", "--"]
CMD ["/bin/bash"]