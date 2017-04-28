############################################################
# Dockerfile for appium grid node setup
# To be connected to existing selenium grid
############################################################

FROM ubuntu:16.04

RUN apt-get -qqy update
RUN apt-get -qqy --no-install-recommends install curl
RUN apt-get -qqy --no-install-recommends install openjdk-8-jdk
RUN apt-get -qqy --no-install-recommends install openjdk-8-jre
RUN apt-get -qqy --no-install-recommends install unzip
RUN apt-get -qqy --no-install-recommends install wget
RUN apt-get -qqy --no-install-recommends install x11vnc

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
ENV ANDROID_BUILD_TOOLS_VERSION=25.0.3
ENV ANDROID_HOME=/root
ENV PATH=$PATH:$JAVA_HOME/bin:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION

EXPOSE 4723
EXPOSE 4444
EXPOSE 5554
EXPOSE 5555
EXPOSE 5556

RUN pwd
RUN wget -O sdkmanager.zip https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip && unzip sdkmanager.zip && rm sdkmanager.zip
RUN find / -type d -name "*tools*" -print
RUN echo y | ./tools/bin/sdkmanager "build-tools;25.0.3"


RUN update-alternatives --config java
RUN update-alternatives --config javac
RUN apt-get autoremove
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN which java
