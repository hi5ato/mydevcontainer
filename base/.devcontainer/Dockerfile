ARG VARIANT="noble"
FROM buildpack-deps:${VARIANT}-curl

LABEL dev.containers.features="common"

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y unminimize && yes | unminimize; apt-get clean

ENV TZ=Asia/Tokyo

RUN apt-get install -y locales
RUN /bin/echo -e "ja_JP.UTF-8 UTF-8\nen_US.UTF-8 UTF-8\nC.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen && \
    /usr/sbin/update-locale LANG=ja_JP.UTF-8
ENV LANG=ja_JP.UTF-8

RUN apt-get install -y --no-install-recommends \
    aptitude less ugrep fzf bat fd-find vim moreutils htop lsof lv lftp zip unzip ncat socat ssh-import-id sudo \
    && apt-get clean

# USERNAME for uid 1000
ARG USERNAME=vscode
RUN if id "ubuntu" &>/dev/null; then \
        echo "Deleting user 'ubuntu'  for ${VARIANT}" && userdel -f -r ubuntu || exit 1; \
    else \
        echo "User 'ubuntu' does not exist for ${VARIANT}"; exit 1; \
    fi;

RUN groupadd -g 1000 $USERNAME
RUN adduser --disabled-password --gecos "" --uid 1000 --gid 1000 $USERNAME
RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME

# brew
RUN apt-get update && apt-get install -y --no-install-recommends git file build-essential && apt-get clean

USER ${USERNAME}
WORKDIR /home/${USERNAME}
RUN NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
ENV PATH="/home/linuxbrew/.linuxbrew/bin:${PATH}"
RUN echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bashrc
RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"; brew doctor && brew install lazygit fish git-credential-oauth

ADD ./ubuntu.sources /home/${USERNAME}

USER root
RUN chsh -s /home/linuxbrew/.linuxbrew/bin/fish ${USERNAME}

# nodejs
RUN curl -fsSL https://deb.nodesource.com/setup_22.x | bash -   && \
    apt-get install -y nodejs && \
    apt-get clean
