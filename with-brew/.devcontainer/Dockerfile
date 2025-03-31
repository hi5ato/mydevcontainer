FROM ghcr.io/hi5ato/codespace-devcontainer-base

ARG DEBIAN_FRONTEND=noninteractive

ENV TZ Asia/Tokyo
ENV LANG ja_JP.UTF-8

RUN apt-get update && apt-get install -y --no-install-recommends build-essential && apt-get clean

USER codespace
WORKDIR /home/codespace
RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
ENV PATH="/home/linuxbrew/.linuxbrew/bin:${PATH}"
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"; brew doctor && brew install fnm hadolint lazydocker lazygit jq yq uv