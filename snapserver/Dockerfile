ARG BUILD_FROM
FROM $BUILD_FROM

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Install required packages
RUN apk add --no-cache \
        pulseaudio alsa-plugins-pulse bash \
        libstdc++ \
        ca-certificates \
        curl \
        unzip

# Install Librespot
RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing/ librespot

# Install Snapcast Server v0.28.0 manually
RUN curl -L -o snapcast.tar.xz https://github.com/badaix/snapcast/releases/download/v0.28.0/snapcast-0.28.0.tar.xz && \
    tar -xf snapcast.tar.xz && \
    cp -av snapcast-0.28.0/snapserver /usr/bin/snapserver && \
    chmod +x /usr/bin/snapserver && \
    rm -rf snapcast*

# Install Snapweb
RUN \
    mkdir -p /usr/share/snapserver/snapweb && \
    curl -L -o snapweb.zip https://github.com/badaix/snapweb/releases/download/v0.8.0/snapweb.zip && \
    unzip -o snapweb.zip -d /usr/share/snapserver/snapweb/ && \
    rm snapweb.zip

# Copy run script
COPY run.sh /
RUN chmod +x /run.sh

CMD [ "/run.sh" ]

#----------------------------Snapserver Ver. 0.0.32 -------------------------------------
# ARG BUILD_FROM
# FROM $BUILD_FROM

# # Set shell
# SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# # hadolint ignore=DL3003
# RUN \
#     apk add --no-cache \
#         pulseaudio alsa-plugins-pulse bash \
#     && rm -fr \
#         /tmp/*
        
# #Install Librespot
# RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/testing/ librespot

# #Install Snapcast
# RUN apk add --no-cache --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community/ snapcast-server

# #Install Snapweb
# RUN \
#     wget https://github.com/badaix/snapweb/releases/download/v0.8.0/snapweb.zip && \
#     unzip -o snapweb.zip -d /usr/share/snapserver/snapweb/ && \
#     rm snapweb.zip

# # Copy data for add-on
# COPY run.sh /
# RUN chmod a+x /run.sh

# CMD [ "/run.sh" ]
