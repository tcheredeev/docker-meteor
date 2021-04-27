FROM node:8
LABEL maintainer="Igor Tcheredeev <tcheredeev@gmail.com> (https://voidozer.ru)"

ENV METEOR_VERSION=1.8.1
ENV METEOR_INSTALLER_SHA256=cc7c6625e549e5ae9eeeb61c860ba6e11222ea6abe921808d495fb13222ba797
ENV METEOR_LINUX_X86_32_SHA256=1de32fd45e5e2ac204ac87711661025135fb351723f7ecd2c7eb2ff304df92eb
ENV METEOR_LINUX_X86_64_SHA256=ea74ae34009c4bf424224cccadaddf73fb8e00d8f3b7f071cb91cc373ed08b98

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
