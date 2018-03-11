FROM ubuntu:14.04
LABEL author="amooly <mooly.xyz@gmail.com>"

#####
#
# startup
#

# prepare a base environment
WORKDIR /root
RUN \
    mkdir tmp && cd tmp

# setup environment variables
ENV LANG C.UTF-8

#####
#
# install package
#

# base package
RUN \
    apt-get update && \
    apt-get install -y \
        curl git-core

# install jdk
RUN \
	apt-get update && \
	apt-get install -y openjdk-7-jre 

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64/jre
ENV PATH $JAVA_HOME:$PATH 

# install hadoop
RUN \
    curl -OL http://apache.01link.hk/hadoop/common/hadoop-3.0.0/hadoop-3.0.0.tar.gz && \
    tar -xzvf hadoop-3.0.0.tar.gz && \
    mv hadoop-3.0.0 /usr/local/hadoop && \
    rm hadoop-3.0.0.tar.gz
ENV HADOOP_HOME=/usr/local/hadoop 
ENV PATH=$PATH:/usr/local/hadoop/bin:/usr/local/hadoop/sbin     

# install zsh & oh-my-zsh
RUN \
    apt-get update && \
    apt-get install -y zsh
RUN \
    git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && chsh -s /bin/zsh

#####
#
# clean temperary folder/cache/package 
#

# remove unnecessary package
RUN \
    apt-get --purge remove -y \
        curl git-core && \
    apt-get autoremove -y \
        curl git-core

# clean cache
RUN \
    dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P &&\
    apt-get clean && sudo apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* 

# remove tmp folder
RUN \
    cd .. && rm -rf tmp
