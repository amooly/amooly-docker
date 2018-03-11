FROM ubuntu:14.04
LABEL author="amooly <mooly.xyz@gmail.com>"

# setup environment variables
ENV LANG C.UTF-8

# install zsh
RUN \
    apt-get update && \
    apt-get install -y \
        curl git-core zsh

# install oh-my-zsh
RUN \
    git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh

# cleanup
RUN \
    apt-get --purge remove -y \
        curl git-core && \
    apt-get autoremove -y \
        curl git-core

# clean caches
RUN \
    dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P &&\
    apt-get clean && sudo apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* 