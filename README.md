# dotfiles

documentation of all my dotfiles, config files, etc

- [$HOME dotfiles](#home-dotfiles)
- [shared dotfiles](#shared-dotfiles)
- [setup $HOME dotfiles](#setup-home-dotfiles)
- [setup shared dotfiles](#setup-shared-dotfiles)

## $HOME dotfiles

### Linux

Ubuntu (bash): https://github.com/gjtiquia/.ubuntu_dotfiles 

Termux (bash): https://github.com/gjtiquia/.termux_dotfiles

### MacOS

MacOS (zsh): https://github.com/gjtiquia/.macos_dotfiles

### Windows

Powershell: https://github.com/gjtiquia/.powershell_dotfiles

WSL (Ubuntu): https://github.com/gjtiquia/.wsl_dotfiles
> technically can have the same as Ubuntu but... just in case lol

Cygwin: https://github.com/gjtiquia/.cygwin_dotfiles

## shared dotfiles

Neovim (btw): https://github.com/gjtiquia/kickstart.nvim

vim (btw): https://github.com/gjtiquia/.vim

lazygit: https://github.com/gjtiquia/lazygit_config

tmux: https://github.com/gjtiquia/.tmux

flameshot: https://github.com/gjtiquia/flameshot_config

ghostty: https://github.com/gjtiquia/ghostty_config

## goals and non-goals

some people like to put all their dotfiles into a single repo

that doesnt work for me, cuz i find that some dotfiles are machine/OS/runtime specific, and some are shared

i prefer a more "modular" approach, where config files are as "self-contained" as possible

this way i can choose individually which dotfiles are "shared", which are not

some people like to use `GNU Stow` for managing their dotfiles

i prefer not to, as i want less dependencies as possible, just plain ol' git, and a consistent setup that works across Windows, MacOS, and Linux

## setup $HOME dotfiles

### preface

these dotfiles live in the $HOME directory

but not all files in the $HOME directory are version controlled

hence there is some git magic to perform in order to make this work, as its not a typical git repo

tldr: bare git repo

the following steps are referenced from this amazing article
- https://www.ackama.com/articles/the-best-way-to-store-your-dotfiles-a-bare-git-repository-explained/

i "could" write a script to run all this but... running this manually "once" isnt too difficult i guess

and... its nice to know under-the-hood whats going on, just in-case

### the steps

setting up git repo
```bash
DOTFILES_HOME=$HOME
DOTFILES_GIT_DIR=.ubuntu_dotfiles # using Ubuntu as an example 

# git init
git init --bare $DOTFILES_HOME/$DOTFILES_GIT_DIR

# set alias
alias dotfiles="git --git-dir=$DOTFILES_HOME/$DOTFILES_GIT_DIR/ --work-tree=$DOTFILES_HOME"

# check setup (should show a lot of untracked files)
dotfiles status

# only keep track of files we explicitly add
dotfiles config --local status.showUntrackedFiles no

# check setup (should not show untracked files)
dotfiles status
```

remember add to .bashrc so it works for new shells
```bash
DOTFILES_HOME=$HOME
DOTFILES_GIT_DIR=.ubuntu_dotfiles 

# set alias
alias dotfiles="git --git-dir=$DOTFILES_HOME/$DOTFILES_GIT_DIR/ --work-tree=$DOTFILES_HOME"
```

adding files to git repo
```bash
dotfiles add .bashrc
dotfiles commit -m "add .bashrc"
```

push to remote
```bash
dotfiles remote add origin <remote-url>
dotfiles push -u origin main
```

installing on new system
```bash
DOTFILES_HOME=$HOME
DOTFILES_GIT_DIR=.ubuntu_dotfiles

# set alias
alias dotfiles="git --git-dir=$DOTFILES_HOME/$DOTFILES_GIT_DIR/ --work-tree=$DOTFILES_HOME"

# .gitignore to prevent weird recursions
echo $DOTFILES_GIT_DIR >> .gitignore

# git clone
git clone --bare <remote-url> $DOTFILES_HOME/$DOTFILES_GIT_DIR

# checkout (handle overwrite files one-by-one manually if needed, eg. by renaming them as a backup, like .bashrc_bak)
dotfiles checkout

# only keep track of files we explicitly add
dotfiles config --local status.showUntrackedFiles no

# check setup (should not show untracked files)
dotfiles status
```

### steps for Cygwin

Cygwin has a lot of weird behavior, so there are some things that you do differently for Cygwin

such as
```bash
# for some reason this is the only way to actually point to $HOME
DOTFILES_HOME=/cygwin64$HOME

# you may need to run this line to prevent issues with line endings
dotfiles config --local core.autocrlf false
```

### steps for Powershell

the above steps are meant to be run on a bash shell

you would need to "translate" them into Powershell commands

see my [Powershell dotfiles](https://github.com/gjtiquia/.powershell_dotfiles/blob/main/OneDrive/Documents/PowerShell/Microsoft.PowerShell_profile.ps1) for an example of how it is "translated"

> side note on terminals and shells on Windows

> Windows Terminal is quite nice to use

> if everything is in WSL, i recommend using WSL

> if the project files are in Windows, i recommend using Powershell.    
> surprisingly a lot of common Linux CLI tools are compiled for Windows too, with package managers like scoop or choco. so its actually quite usable. can be configured to "feel at home" like in Linux    
> Powershell makes it "feel more at home" compared to Command Prompt (cmd), so i recommend Powershell over Command Prompt too. (eg. you can use commands like `ls`)    
> although, it is worth exploring, whether the project files can fully be in Linux as well. if so, it might be worth just migrating everything to Linux and either use WSL, use a VM, or go full Linux with dual booting.

> i dont recommend using Cygwin.    
> for "basic" use cases its ok. for more "advanced" things, you start to run into limitations and hacks. you can pretty much achieve whatever you need with either WSL or Powershell

## setup shared dotfiles

see each repo for setup steps, i probably documented them there

but most likely, they are either a self contained directory in `$HOME` or `$HOME/.config`

so just do regular git cloning would suffice. just be aware of correct directory naming.
