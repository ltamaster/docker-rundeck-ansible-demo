ARG RUNDECK_IMAGE

FROM ${RUNDECK_IMAGE}
USER root

RUN echo "deb http://archive.ubuntu.com/ubuntu xenial-updates main restricted universe multiverse /" | sudo tee -a /etc/apt/sources.list

RUN apt-get -y update && \
    apt-get -y install \
    software-properties-common  \
    apt-transport-https \
    iputils-ping \
    openssh-server \
    netcat-traditional \
    unzip \
    zip \
    jq \
    bsdmainutils \
    wamerican \
    sysstat \
    vim \
    build-essential


# install ansible
RUN apt-get -y install sshpass && \
    apt-get -y install python3-pip && \
    apt-get -y install python-pip && \
    pip3 install --upgrade pip

RUN pip3 install ansible

USER rundeck

RUN mkdir data
#COPY --chown=rundeck:root ./data/id_rsa $RDECK_BASE/.ssh/id_rsa
#COPY --chown=rundeck:root ./data/id_rsa.pub $RDECK_BASE/.ssh/id_rsa.pub
#RUN chmod 600 $RDECK_BASE/.ssh/id_rsa

