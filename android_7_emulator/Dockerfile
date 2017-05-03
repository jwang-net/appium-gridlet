FROM android-node-base

ENV ANDROID_SDK_VERSION=25 \
    ANDROID_ABI=google_apis/armeabi-v7a

RUN echo n | android create avd --force -n android_api_${ANDROID_SDK_VERSION} -t 1 --abi ${ANDROID_ABI} \
    emulator64-arm -avd android_api_${ANDROID_SDK_VERSION} -no-boot-anim -no-window -noaudio -gpu off
