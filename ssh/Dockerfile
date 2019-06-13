FROM ubuntu:latest
# latest LTS

RUN apt-get -y update && \
    apt-get -y install sudo  && \
    apt-get -y install openssh-server && \
    apt-get -y install \
        unzip \
        curl \
        xmlstarlet \
        git \
        netcat-traditional \
        uuid-runtime \
        ncurses-bin \
        iputils-ping \
        net-tools \
        jq \
        zip \
        python \
        wget \
        python-requests \
        libjson-maybexs-perl \
        libyaml-perl \
        sysstat

RUN mkdir /var/run/sshd
RUN mkdir /configuration

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
RUN sed -i "s/.*PasswordAuthentication.*/PasswordAuthentication yes/g" /etc/ssh/sshd_config

ENV USERNAME=rundeck
ENV HOME=/home/rundeck

RUN adduser --home $HOME  --disabled-password  --gecos "Rundeck" $USERNAME
RUN echo 'rundeck:rundeck' | chpasswd

RUN echo 'rundeck ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers


COPY setup /tmp/setup

RUN /tmp/setup/mk_rundeck_user

COPY rdeck_ssh_start /usr/local/sbin

EXPOSE 22

# CMD /usr/sbin/sshd -e -D
CMD /usr/local/sbin/rdeck_ssh_start