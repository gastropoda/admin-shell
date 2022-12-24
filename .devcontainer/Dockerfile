FROM rockylinux:9.1
RUN dnf update -y \
  && dnf install -y \
    git \
  && dnf clean all
RUN useradd --create-home --shell /bin/bash devops
USER devops
