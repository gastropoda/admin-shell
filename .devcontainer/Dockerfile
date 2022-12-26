ARG image_version=9.1
FROM rockylinux:$image_version
RUN dnf update -y \
  && dnf upgrade --refresh -y \
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
ENV container_state_dir=/home/$container_user/.local/var/state
RUN mkdir -p $container_state_dir
ENV HISTFILE=$container_state_dir/bash_history
