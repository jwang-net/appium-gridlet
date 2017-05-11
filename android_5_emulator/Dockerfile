FROM android-node-base

COPY entrypoint.sh / \
     android_5_node.json /
RUN chmod +x /entrypoint.sh \
    chmod +x /android_5_node.json
ENTRYPOINT ["/entrypoint.sh"]

ENV ANDROID_SDK_VERSION=22 \
    ANDROID_ABI=google_apis/armeabi-v7a

RUN echo ${HUB_HOST}
RUN echo ${HUB_PORT}
RUN echo ${HUB_IP}
RUN echo ${ANDROID_HOME}
RUN nohup appium --nodeconfig /android_5_node.json -a ${HUB_HOST} -p ${HUB_PORT} --session-override &
RUN echo n | android create avd --force -n android_api_${ANDROID_SDK_VERSION} -t 1 --abi ${ANDROID_ABI} && \
    echo n | nohup emulator64-arm -avd android_api_${ANDROID_SDK_VERSION} -no-boot-anim -no-window -noaudio -gpu off &
