FROM jenkins/jenkins:2.107.2-alpine

#ENV http_proxy=${http_proxy} \
#    https_proxy=${https_proxy} \
#    no_proxy="${no_proxy}"

RUN echo 2.73.3 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state && \
    echo 2.73.3 > /usr/share/jenkins/ref/jenkins.install.InstallUtil.lastExecVersion

USER root

ENV GLIBC 2.28-r0

# Fix for avoiding docker-compose installation via pip
RUN apk add --no-cache wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk && \
    apk add --no-cache glibc-2.28-r0.apk && rm glibc-2.28-r0.apk && \
    ln -s /lib/libz.so.1 /usr/glibc-compat/lib/ && \
    ln -s /lib/libc.musl-x86_64.so.1 /usr/glibc-compat/lib 

RUN curl -L https://get.docker.com/builds/Linux/x86_64/docker-1.10.3 -o /usr/local/bin/docker && \
    chmod +x /usr/local/bin/docker && \
    curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

COPY plugins_list.txt /tmp
RUN /usr/local/bin/install-plugins.sh $(cat /tmp/plugins_list.txt | tr '\n' ' ')

COPY *.groovy /usr/share/jenkins/ref/init.groovy.d/
