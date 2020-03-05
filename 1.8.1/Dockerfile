FROM node:8
LABEL maintainer="Igor Tcheredeev <tcheredeev@gmail.com> (https://voidozer.ru)"

ENV METEOR_VERSION=1.8.1
ENV METEOR_INSTALLER_SHA256=b3d9fce98719cabec4a5bded1abd4d240316096e62723276522dde724184d182
ENV METEOR_LINUX_X86_32_SHA256=433005f3cb847bb8c9363291efceba17174aca7dd5c233dd2af1747527b6e18e
ENV METEOR_LINUX_X86_64_SHA256=8691816f157f97f10ea7070f72faa3d5f55e6ffe462576e4fd10dfd0844485e2

# 1. Download & verify the meteor installer.
# 2. Patch it to validate the meteor tarball's checksums.
# 3. Install meteor

COPY meteor-installer.patch /tmp/meteor/meteor-installer.patch
COPY vboxsf-shim.sh /usr/local/bin/vboxsf-shim
RUN echo ${METEOR_VERSION}
RUN echo ${METEOR_INSTALLER_SHA256}
RUN mkdir -p /tmp/meteor
RUN curl -SL https://install.meteor.com/ -o /tmp/meteor/inst
RUN sed -e "s/^RELEASE=.*/RELEASE=\"${METEOR_VERSION}\"/" /tmp/meteor/inst > /tmp/meteor/inst-canonical
RUN echo $METEOR_INSTALLER_SHA256 /tmp/meteor/inst-canonical | sha256sum -c
RUN patch /tmp/meteor/inst /tmp/meteor/meteor-installer.patch
RUN chmod +x /tmp/meteor/inst
RUN /tmp/meteor/inst
RUN rm -rf /tmp/meteor

VOLUME /app
WORKDIR /app
EXPOSE 3000
CMD [ "meteor" ]
