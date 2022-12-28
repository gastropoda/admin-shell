ARG image_version=9.1
FROM rockylinux:$image_version
RUN dnf update -y \
  && dnf install epel-release -y \
  && dnf update -y \
  && dnf upgrade --refresh -y \
  && dnf install -y \
    bind-utils \
    findutils \
    git \
    iproute \
    iputils \
    lastpass-cli \
    mtr \
    procps-ng \
    socat \
    traceroute \
  && dnf clean all

ARG container_user=devops
RUN useradd --create-home --shell /bin/bash $container_user
USER $container_user
RUN mkdir -p /home/$container_user/{.local/state,.local/share,.cache}
ENV HISTFILE=/home/$container_user/.local/state/bash_history

# lastpass-cli attempts to follow XDG specification but fails.
# help it comply
ENV LPASS_HOME=/home/$container_user/.local/share/lpass
RUN mkdir -p $LPASS_HOME
