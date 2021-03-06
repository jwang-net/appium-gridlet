FROM ubuntu:16.04

WORKDIR /root

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true
ENV JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
ENV PATH=$PATH:$JAVA_HOME/bin

# apt-get dependencies
RUN apt-get update -qqy
RUN apt-get -qqy --no-install-recommends install
RUN apt-get -qqy --no-install-recommends install ca-certificates \
    openjdk-8-jre-headless && \
    sed -i 's/securerandom.source=file:\/dev\/urandom/securerandom.source=file:\/dev\/.\/urandom/g' \
       /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/java.security && \
    sed -i 's/securerandom.source=file:\/dev\/random/securerandom.source=file:\/dev\/.\/urandom/g' \
       /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/java.security && \
    apt-get -qyy autoremove && \
    rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN apt-get update -qqy && \
    apt-get -qqy --no-install-recommends install \
    tzdata \
    curl \
    xvfb \
    x11vnc \
    wget \
    libqt5webkit5 \
    unzip && \

# set java home
  { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home && \
	chmod +x /usr/local/bin/docker-java-home && \
  apt-get -qyy autoremove && \
  rm -rf /var/lib/apt/lists/* /var/cache/apt/*

ENV ANDROID_BUILD_TOOLS_VERSION=25.0.3 \
    ANDROID_HOME=/root

ENV PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$ANDROID_HOME/build-tools/$ANDROID_BUILD_TOOLS_VERSION

# install android build-tools, and sdks 25 (Android 7), 23 (Android 6), 22 (Android 5)
# install abis for all relevant android sdks
RUN wget -O tools.zip https://dl.google.com/android/repository/tools_r25.2.3-linux.zip && \
    unzip tools.zip && rm tools.zip && \
    echo y | android update sdk -a -u -t platform-tools,build-tools-${ANDROID_BUILD_TOOLS_VERSION} && \
    echo y | android update sdk -a -u -t android-25,sys-img-armeabi-v7a-google_apis-25 && \
    echo y | android update sdk -a -u -t android-22,sys-img-armeabi-v7a-google_apis-22 && \
    chmod a+x -R $ANDROID_HOME && \
    chown -R root:root $ANDROID_HOME

# get latest stable version of appium
ENV APPIUM_VERSION=1.6.3 \
    UDEV_REMOTE_FILE=https://raw.githubusercontent.com/M0Rf30/android-udev-rules/master/51-android.rules

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash - && \
    apt-get -qqy install nodejs && \
    npm install -g appium@${APPIUM_VERSION} --no-shrinkwrap  && \
    npm cache clean && \
    apt-get remove --purge -y npm && \
    apt-get autoremove --purge -y && \
    mkdir /etc/udev/rules.d && \
    wget --no-verbose $UDEV_REMOTE_FILE -O /etc/udev/rules.d/51-android.rules && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get clean

# expose ports of appium and default emulator port
EXPOSE 4723
EXPOSE 5900
EXPOSE 5554
