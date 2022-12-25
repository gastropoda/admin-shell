ARG image_version=9.1
FROM rockylinux:$image_version
RUN dnf update -y \
  && dnf install -y \
    bind-utils \
    git \
    iproute \
    iputils \
    mtr \
    traceroute \
  && dnf clean all

ARG container_user=devops
RUN useradd --create-home --shell /bin/bash $container_user
USER $container_user
RUN mkdir -p ~/.local/var/state
