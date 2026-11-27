ARG DEBIAN_BASE_IMAGE_NAME
ARG DEBIAN_BASE_IMAGE_REGISTRY
ARG DEBIAN_BASE_IMAGE_VERSION
FROM ${DEBIAN_BASE_IMAGE_REGISTRY}/${DEBIAN_BASE_IMAGE_NAME}:${DEBIAN_BASE_IMAGE_VERSION}

RUN apt-get update \
 && apt-get install -y \
      cron \
      rsync \
 && rm -rf /usr/share/{doc,info,man} \
 && rm -rf /usr/local/share/{doc,info,man} \
 && sed -i 's/session    required     pam_loginuid.so//g' /etc/pam.d/cron

COPY localtime /etc/localtime
COPY run-cron /
COPY cron-script /
COPY excludes /

CMD ["/run-cron"]
