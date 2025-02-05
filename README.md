# About
This is my personal repository to manage and distribute my dotfiles with just git. Feel free to fork and adjust it to your needs.

# Setup
Fork this repository to customize it to your needs. The setup dotfile management is set up like described in [this guide](https://www.atlassian.com/git/tutorials/dotfiles). Additionally to the the article the [dotbare](https://github.com/kazhala/dotbare) zsh plugin is installed to enhance the management of the bare repository. Here is a condensed version for you:

1. Alias in .zshrc (you will need to set the alias for current session or restart your terminal):
```
alias config='/usr/bin/git --git-dir=$HOME/.cfg --work-tree=$HOME'
```
2. Prevent recursion problems
```
$ mkdir -p ~/.config/git
$ echo "~/.cfg" >> .config/git/ignore
```
3. Clone your dotfiles repository. If you have conflicting files while config checkout, then backup/move them away.
```
$ git clone --bare <git-repo-url> $HOME/.cfg
$ config checkout
```
4. Don't show untracked files
```
$ config config --local status.showUntrackedFiles no
```
5. Switch alias in .zshrc to dotbare (you will need to set the alias for current session or restart your terminal):
```
$ alias config='dotbare'
```

# Workflow
You can use config commands to add and update your dotfiles.
```
$ config status
$ config add .vimrc
$ config commit -m "Add vimrc"
$ config add .bashrc
$ config commit -m "Add bashrc"
$ config push
```
dotbare provides a series of scripts starts with a prefix f (e.g. `dotbare fadd`, `dotbare flog` etc) that will enable a interactive experience by processing all the git information and display it through `fzf`. In addition, `dotbare` also comes with command line completion that you could choose to either to complete `git` commands or `dotbare` commands.