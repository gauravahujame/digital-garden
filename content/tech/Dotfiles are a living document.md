---
title: Dotfiles are a living document
tags:
  - budding
  - tools
  - terminal
---

Your dotfiles (`.zshrc`, `.gitconfig`, editor and terminal configs) record how you like to work. Treat them like a garden: commit them, prune them, and change them a little at a time.

## Why version them

- **New machine in minutes.** Clone, run one command, and you're home.
- **History of your taste.** `git log` shows when you switched from bash to zsh, and why.
- **Safe experiments.** Try a new prompt or keybinding. If it's bad, `git revert`.

## Two common approaches

| | GNU Stow | chezmoi |
|---|---|---|
| Mechanism | Symlinks files from a repo into `$HOME` | Renders files from a source dir into `$HOME` |
| Per-machine differences | Separate packages, or branches | Templates (`{{ if eq .chezmoi.os "darwin" }}`) |
| Secrets | Keep them out of the repo yourself | Integrates with password managers |
| Learning curve | Very low | Moderate |

Stow is great when your machines are similar. chezmoi pays off once you have a work laptop, a personal laptop, and a Linux server that all need slightly different configs.

## A minimal Stow layout

```text
~/dotfiles
├── zsh/
│   └── .zshrc
├── git/
│   └── .gitconfig
└── nvim/
    └── .config/nvim/init.lua
```

```bash
cd ~/dotfiles
stow zsh git nvim   # creates the symlinks in $HOME
```

## Rules I try to follow

1. **Comment the why, not the what.** `# disable because it breaks tmux copy mode` is useful a year later. `# set option` is not.
2. **Delete aggressively.** If you don't remember what a line does, remove it and see what breaks.
3. **Never commit secrets.** Load tokens from a password manager or a git-ignored `~/.secrets` file.
4. **Start small.** Copying someone's 2,000-line config breaks [[ideas/Gall's law]]. Borrow one idea at a time.

> [!tip] Keep startup fast
> Run `time zsh -i -c exit` occasionally. If shell startup creeps past a few hundred milliseconds, lazy-load the slow parts (version managers are the usual culprits).

Related: [[tech/Deep modules]]. A good alias or function is a tiny deep module: one short name that hides a long command.
