ARG DEBIAN_BASE_IMAGE_NAME=debian
ARG DEBIAN_BASE_IMAGE_REGISTRY=docker.io/library
ARG DEBIAN_BASE_IMAGE_VERSION=stable
FROM ${DEBIAN_BASE_IMAGE_REGISTRY}/${DEBIAN_BASE_IMAGE_NAME}:${DEBIAN_BASE_IMAGE_VERSION}

RUN apt-get update \
 && apt-get dist-upgrade --auto-remove --purge --yes \
 && apt-get install --no-install-recommends --yes \
      cron \
      debmirror \
      ed \
      patch \
 && apt-get distclean \
 && rm -rf /usr/share/{doc,info,man} \
 && rm -rf /usr/local/share/{doc,info,man} \
 && sed -i 's/session    required     pam_loginuid.so//g' /etc/pam.d/cron

COPY localtime /etc/localtime
COPY run-cron /
COPY cron-script /
COPY mirror /

CMD [ "/run-cron" ]
