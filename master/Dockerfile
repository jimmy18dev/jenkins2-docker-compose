FROM jenkins/jenkins:lts

LABEL maintainer="jimmy18dev@gmail.com"

USER root

# Install some useful packages
RUN apt-get update && apt-get --no-install-recommends --no-install-suggests --yes --quiet install apt-transport-https bash-completion ca-certificates curl git gnupg imagemagick less gnupg2 software-properties-common make mysql-client perceptualdiff procps ssh-client sudo vim wget && apt-get clean && apt-get --yes --quiet autoremove --purge

# Install Docker CE
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update && apt-get install docker-ce -y
RUN docker --version

# cleaning
RUN rm -rf  /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/groff/* /usr/share/info/* /usr/share/linda/* /usr/share/lintian/* /usr/share/locale/* /usr/share/man/*

# TimeZone
ENV TZ=Asia/Bangkok
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins

ENV JAVA_OPTS="-Xmx8192m"
ENV JENKINS_OPTS=" --handlerCountMax=300"

# Add user jenkins to list of sudoers
RUN usermod -a -G root jenkins

# Switch to user jenkins
USER jenkins