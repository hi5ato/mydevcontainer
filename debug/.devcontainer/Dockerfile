ARG VARIANT="noble"
FROM buildpack-deps:${VARIANT}-curl

LABEL dev.containers.features="common"

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN yes | unminimize; apt-get clean

RUN apt-get install -y man-db less

RUN userdel -f -r ubuntu
