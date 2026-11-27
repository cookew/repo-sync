FROM docker.io/rockylinux/rockylinux:10-ubi

RUN dnf update -y \
  && dnf install -y \
    cronie \
    yum-utils \
  && dnf clean all \
  && rm -rf /usr/local/share/{doc,info,man}/* \
  && rm -rf /usr/share/{doc,info,man/man*}/* \
  && rm -rf /var/cache/dnf/* \
  && rm -rf /var/log/dnf* \
  && mkdir /pid \
  && ln -s /pid/crond.pid /run/crond.pid \
  && useradd -s /bin/bash repo \
  && touch /pid/crond.pid \
  && chown repo:repo /pid/crond.pid

COPY cron-script /
COPY repos.d /repos.templates
COPY run-cron /

USER repo

VOLUME /etc/yum.repos.d
VOLUME /pid
VOLUME /repos
VOLUME /repos.d
VOLUME /repo-mirror
VOLUME /var/spool/cron
VOLUME /var/tmp

CMD ["/run-cron"]
