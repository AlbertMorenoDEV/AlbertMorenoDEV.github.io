---
layout: post
title: "Initial setup for a new macOS computer"
categories: macos apple
---

## System Preferences

### Keyboard

- Set key repeat to fast and delay until repeat to almost fast.

### Dock

- Set size to small.
- Remove workspace auto-switching by running the following command:
> defaults write com.apple.dock workspaces-auto-swoosh -bool NO
> killall Dock # Restart the Dock process

### Finder

- Change New finder window show to open in your Home Directory
- Add Home and your Code Directory to the sidebar

### Menubar

- Remove bluetooth and display icons
- Change battery to show percentage
- Add sound icon
- Install runcat, amphetamine and monosnap

### Spotlight

- Uncheck contancts, events, films, fonts, images and music.

### Accounts

- Add an iCloud account and sync Calendar, Find my Mac, Contacts etc.

## Xcode

> xcode-select --install

## Homebrew

> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
> echo 'PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Test it:
> brew doctor

### Cask

Homebrew-Cask extends Homebrew and allows you to install large binary files via a command-line tool. You can for example install applications like Google Chrome, Dropbox, VLC and Spectacle. No more downloading .dmg files and dragging them to your Applications folder!

#### Quick Look plugins

> brew cask install \
      qlcolorcode \
      qlstephen \
      qlmarkdown \
      quicklook-json \
      qlprettypatch \
      quicklook-csv \
      betterzip \
      webpquicklook \
      suspicious-package \
      muzzle

#### App Suggestions

> brew cask install \
      appcleaner \
      cheatsheet \
      docker \
      firefox \
      google-chrome \
      spotify \
      zoomus \
      phpstorm \
      goland \
      evernote \
      monosnap \
      amphetamine \
      runcat \
      postman \
      slack \
      iterm2 \
      mysqlworkbench \
      tree

### Brewfile

Dump current packages: `brew bundle dump`
Restore packages: `brew bundle`

## iTerm 2

> brew cask install iterm2

### Setup

- Set hot-key to open and close the terminal to `command + option + i`
- Go to profiles -> Default -> Terminal -> Check silence bell to disable the terminal session from making any sound
- Download one of [iTerm2 color schemes](https://github.com/mbadolato/iTerm2-Color-Schemes/tree/master/schemes) and then set these to your default profile colors
- Change the cursor text and cursor color to yellow make it more visible
- iTerm → Preferences → Profiles → Keys → Presets... → Natural Text Editing

## ZSH

> brew install zsh

### Oh My Zsh

> sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
> chsh -s $(which zsh)

#### Recommended plugins

> plugins=(git git-extras osx colorize history zsh-completions zsh-autosuggestions zsh-syntax-highlighting zsh-iterm-touchbar)

#### Recommended themes

- powerlevel9k
- [powerlevel10k](https://github.com/romkatv/powerlevel10k)
> git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

## fzf

[fzf](https://github.com/junegunn/fzf) is a general-purpose command-line fuzzy finder.

> brew install fzf

### Example Usages

```bash
# fd - cd to selected directory
fd() {
  local dir
  dir=$(find ${1:-.} -path '*/\.*' -prune \
                  -o -type d -print 2> /dev/null | fzf +m) &&
  cd "$dir"
}
```

```bash
# fh - search in your command history and execute selected command
fh() {
  eval $( ([ -n "$ZSH_NAME" ] && fc -l 1 || history) | fzf +s --tac | sed 's/ *[0-9]* *//')
}
```

```bash
# ch - browse chrome history
ch() {
  local cols sep
  cols=$(( COLUMNS / 3 ))
  sep='{::}'

  cp -f ~/Library/Application\ Support/Google/Chrome/Profile\ 1/History /tmp/h

  sqlite3 -separator $sep /tmp/h \
    "select substr(title, 1, $cols), url
     from urls order by last_visit_time desc" |
  awk -F $sep '{printf "%-'$cols's  \x1b[36m%s\x1b[m\n", $1, $2}' |
  fzf --ansi --multi | sed 's#.*\(https*://\)#\1#' | xargs open
}
```

```bash
# dc - browse running Docker containers
dc() {
  if docker ps > /dev/null 2>&1; then
      container=$(docker ps | awk '{if (NR!=1) print $1 ": " $(NF)}' | fzf --height 40%)
  
      if [[ -n $container ]]; then
          container_id=$(echo $container | awk -F ': ' '{print $1}')
  
          docker exec -it $container_id /bin/bash -lc "export TERM=xterm; stty rows 50 cols 120; exec bash"
      else
          echo "You haven't selected any container! ༼つ◕_◕༽つ"
      fi
  else
      echo "Docker daemon is not running! (ಠ_ಠ)"
  fi
}
```

## tree

> brew install tree

## Bash Completion

> brew install bash-completion
> echo "\n# Bash Completion\n[[ -r \"/usr/local/etc/profile.d/bash_completion.sh\" ]] && . \"/usr/local/etc/profile.d/bash_completion.sh\"" >> ~/.zshrc
> brew install docker-completion docker-compose-completion

## Sources of this guide
- https://sourabhbajaj.com/mac-setup/