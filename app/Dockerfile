FROM centos:7

WORKDIR /usr/src/app

ENV JDK_VERSION 1.8.0
ENV MVN_VERSION 3.5.4
ENV TZ Australia/Sydney

RUN rm -rf /etc/localtime && \
	ln -s /usr/share/zoneinfo/$TZ /etc/localtime

RUN echo "date:"
RUN date "+%H:%M:%S   %d/%m/%y"

RUN	yum -y group install "Development Tools" && \
	echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf && \
    yum -y install \
    docker \
    atomic-openshift-clients \
	  java-$JDK_VERSION-openjdk-devel \
	  unzip

# Add Node repo and install node
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
RUN yum -y install nodejs
# Install yaml validator package used for config health checks
RUN npm install --global yaml-validator

VOLUME ["/var/run/docker.sock"]

# GIT configuration
#COPY conf/.gitconfig $BUILDKITE_USER_HOME
#RUN chmod 644 $BUILDKITE_USER_HOME/.gitconfig

# INSTALL MAVEN
RUN curl -O http://apache.mirror.serversaustralia.com.au/maven/maven-3/$MVN_VERSION/binaries/apache-maven-$MVN_VERSION-bin.tar.gz && \
    tar xvzf apache-maven-$MVN_VERSION-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-$MVN_VERSION /opt/apache-maven && \
    ln -s /opt/apache-maven/bin/mvn /usr/local/bin/mvn && \
    rm -rf apache-maven-$MVN_VERSION-bin.tar.gz
    
