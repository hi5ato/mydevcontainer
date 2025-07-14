# Devcontainer for local development

ghcr.io/hi5ato/mydevcontainer:latest

## Version

* ubuntu noble
* nodejs 22

## basic config

```bash
ssh-import-id-gh hi5ato
sudo update-alternatives --config editor
sudo update-alternatives --config pager
```

## user

```bash
sudo su - vscode
```

### Homebrew

### fish

```fish
alias -s less "less -i"
read -U GH_CODESPACE_TOKEN_FOR_PUSH
```

#### edit fish config

```fish

vim ~/.config/fish/config.fish

# ~/.config/fish/config.fish
if status is-interactive
     # Commands to run in interactive sessions can go here
     # ・
     # ・（他にコマンドがあればここに記述されているはず）
     # ・

    # 以下を追加
    eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
end

if not string match -q "$TERM_PROGRAM" "vscode"
    fundle plugin IlanCosman/tide@v6
end

fundle plugin jethrokuan/z
fundle plugin jethrokuan/fzf
fundle plugin 0rax/fish-bd
fundle plugin decors/fish-ghq
# fundle plugin halostatue/fish-docker@v1.x
# fundle plugin IlanCosman/tide@v5.0.1
fundle init

string match -q "$TERM_PROGRAM" "vscode"
    and . (code --locate-shell-integration-path fish)

set PATH $PATH /home/lala/.local/bin
```

***and apply***

```fish
source ~/.config/fish/config.fish
```

#### install fundle

```fish
curl -sfL https://git.io/fundle-install | fish
```

## install other apps

```fish
brew install fnm hadolint lazydocker lazygit jq yq uv
```
