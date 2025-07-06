# Start from a base Debian image with Java pre-installed
FROM mcr.microsoft.com/devcontainers/java:1-17-bullseye

# Install necessary packages and download Android SDK
ARG ANDROID_SDK_VERSION=11076708
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y --no-install-recommends wget unzip libncurses5 sudo \
    && wget -q https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_SDK_VERSION}_latest.zip -O /tmp/cmdline-tools.zip \
    && mkdir -p /usr/lib/android-sdk/cmdline-tools \
    && unzip -q /tmp/cmdline-tools.zip -d /usr/lib/android-sdk/cmdline-tools \
    && mv /usr/lib/android-sdk/cmdline-tools/cmdline-tools /usr/lib/android-sdk/cmdline-tools/latest \
    && rm /tmp/cmdline-tools.zip \
    && yes | /usr/lib/android-sdk/cmdline-tools/latest/bin/sdkmanager --licenses > /dev/null \
    && /usr/lib/android-sdk/cmdline-tools/latest/bin/sdkmanager "platforms;android-34" "build-tools;34.0.0" "platform-tools" > /dev/null \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Set up Environment Variables
ENV ANDROID_HOME=/usr/lib/android-sdk
ENV ANDROID_SDK_ROOT=${ANDROID_HOME}
ENV PATH=${PATH}:${ANDROID_HOME}/cmdline-tools/latest/bin:${ANDROID_HOME}/platform-tools
