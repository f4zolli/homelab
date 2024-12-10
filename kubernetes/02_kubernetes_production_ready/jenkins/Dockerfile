# ref:
# https://medium.com/@lilnya79/building-jenkins-image-with-docker-cli-preinstalled-for-seamless-devops-integration-ec185f76755b
FROM jenkins/jenkins:latest

USER root

RUN apt-get update && \
    apt-get install -y sudo vim curl wget

RUN echo 'root:abc123' | chpasswd

RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN apt-get update && \
    apt-get install -y apt-transport-https \
                       ca-certificates \
                       gnupg2 \
                       curl \
                       software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc && \
    chmod a+r /etc/apt/keyrings/docker.asc && \
    echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install docker-ce-cli -y

RUN groupadd docker

RUN usermod -aG docker jenkins

USER jenkins