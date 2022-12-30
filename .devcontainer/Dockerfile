ARG image_version=9.1
FROM rockylinux:$image_version
RUN dnf update -y \
  && dnf install epel-release -y \
  && dnf update -y \
  && dnf upgrade --refresh -y \
  && dnf install -y \
    bind-utils \
    e2fsprogs \
    findutils \
    git \
    iproute \
    iputils \
    lastpass-cli \
    mtr \
    procps-ng \
    socat \
    sudo \
    traceroute \
    unzip \
    wget \
  && dnf clean all

# WSL base image specific, to extract into its own image later
ADD wsl.conf resolv-default.conf /etc

RUN sed -ir '/%wheel/s/^#? */# /;/%wheel.*NOPASS/s/^# *//' /etc/sudoers

ARG container_user=devops
RUN groupadd docker
RUN useradd --create-home --shell /bin/bash --groups wheel,docker \
  $container_user
USER $container_user
RUN mkdir -p /home/$container_user/{.local/state,.local/share,.cache}
ENV HISTFILE=/home/$container_user/.local/state/bash_history

# lastpass-cli attempts to follow XDG specification but fails.
# help it comply
ENV LPASS_HOME=/home/$container_user/.local/share/lpass
RUN mkdir -p $LPASS_HOME

ARG ohmyposh_base_url=https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download
RUN mkdir -p /home/$container_user/.local/bin \
  && curl $ohmyposh_base_url/posh-linux-amd64 \
    -Lo /home/$container_user/.local/bin/oh-my-posh \
  && chmod 0744 /home/$container_user/.local/bin/oh-my-posh \
  && mkdir /home/$container_user/.poshthemes \
  && curl $ohmyposh_base_url/themes.zip \
    -Lo /home/$container_user/.poshthemes/themes.zip \
  && unzip /home/$container_user/.poshthemes/themes.zip \
    -d /home/$container_user/.poshthemes \
  && chmod u+rw /home/$container_user/.poshthemes/*.omp.* \
  && rm /home/$container_user/.poshthemes/themes.zip
