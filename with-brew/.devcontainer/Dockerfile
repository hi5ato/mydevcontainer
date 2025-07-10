FROM ghcr.io/hi5ato/mydevcontainer-base

ARG DEBIAN_FRONTEND=noninteractive

ENV TZ=Asia/Tokyo
ENV LANG=ja_JP.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends build-essential && apt-get clean
# RUN chsh -s /usr/bin/fish vscode

USER vscode
WORKDIR /home/vscode
RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
ENV PATH="/home/linuxbrew/.linuxbrew/bin:${PATH}"
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"; brew doctor && brew install lazygit fish git-credential-oauth

USER root
RUN chsh -s /home/linuxbrew/.linuxbrew/bin/fish vscode