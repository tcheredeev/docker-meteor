FROM node:12
MAINTAINER Igor Tcheredeev (https://voidozer.ru/)

ENV METEOR_VERSION 1.8.1
ENV METEOR_INSTALLER_SHA256 b3d9fce98719cabec4a5bded1abd4d240316096e62723276522dde724184d182
ENV METEOR_LINUX_X86_32_SHA256 latest
ENV METEOR_LINUX_X86_64_SHA256 latest

# 1. Download & verify the meteor installer.
# 2. Patch it to validate the meteor tarball's checksums.
# 3. Install meteor

COPY meteor-installer.patch /tmp/meteor/meteor-installer.patch
COPY vboxsf-shim.sh /usr/local/bin/vboxsf-shim
RUN curl -SL https://install.meteor.com/ -o /tmp/meteor/inst \
    && sed -e "s/^RELEASE=.*/RELEASE=\"\$METEOR_VERSION\"/" /tmp/meteor/inst > /tmp/meteor/inst-canonical \
    && echo $METEOR_INSTALLER_SHA256 /tmp/meteor/inst-canonical | sha256sum -c \
    && patch /tmp/meteor/inst /tmp/meteor/meteor-installer.patch \
    && chmod +x /tmp/meteor/inst \
    && /tmp/meteor/inst \
    && rm -rf /tmp/meteor

VOLUME /app
WORKDIR /app
EXPOSE 3000
CMD [ "meteor" ]
