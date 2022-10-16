---
title: "Ec2 Shell Setup"
date: 2022-10-16T18:11:12+09:00
draft: false
---

## 概要

- [さんこう](https://blog.serverworks.co.jp/setting-dev-ec2-rails-app#%E3%83%97%E3%83%AD%E3%83%B3%E3%83%97%E3%83%88starship%E3%81%AE%E8%A8%AD%E5%AE%9A)
- デフォルトシェルにzsh
    - auto-suggestion
    - syntax-highlighting
- プロンプトをstarshipに
- exa, bat

## installation

```bash
# zsh
sudo yum install zsh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.zsh/zsh-syntax-highlighting

# starship
sudo su
curl -sS https://starship.rs/install.sh | sh
exit

# bat, exa
cargo install exa
cargo install bat
```

- ~/.zshrc

```bash
autoload -Uz colors
colors

HISTFILE=~/.zsh_history
HISTSIZE=100000
SAVEHIST=100000
setopt share_history
setopt hist_ignore_dups
setopt hist_ignore_all_dups

source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh
source ~/.zsh/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

alias ls="exa --icons"
alias cat="bat --paging=never"

source ~/.cargo/env

eval "$(starship init zsh)"
```

- デフォルトシェル変更

```bash
sudo yum install util-linux-user
sudo chsh ec2-user
```

- ~/.config/starship.toml

```bash
[directory]
truncation_length = 100
truncate_to_repo = false
```