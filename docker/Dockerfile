FROM jenkins/jenkins:lts

USER root

RUN apt-get update && \
    apt-get install -y sudo curl && \
    rm -rf /var/lib/apt/lists/*

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers && \
    curl -fsSL https://get.docker.com -o get-docker.sh && \
    sh get-docker.sh && \
    usermod -aG docker jenkins

COPY daemon.json /etc/docker

USER jenkins