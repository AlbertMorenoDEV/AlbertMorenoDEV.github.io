---
layout: post
title: "Dotfiles setup"
categories: macos apple
---

> cd
> git init --bare $HOME/dotfiles
> echo "alias config='/usr/bin/git --git-dir=$HOME/dotfiles --work-tree=$HOME'" >> $HOME/.bashrc
> bash
> config config --local status.showUntrackedFiles no
> config remote add origin git@github.com:AlbertMorenoDEV/dotfiles.git
> config add .zshrc
> ...

## [dotbare](https://github.com/kazhala/dotbare)

> git clone https://github.com/kazhala/dotbare.git $HOME/.oh-my-zsh/custom/plugins/dotbare

## Sources
- https://www.youtube.com/watch?v=tBoLDpTWVOM
- https://www.atlassian.com/git/tutorials/dotfiles