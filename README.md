# dotfiles

documentation of all my dotfiles, config files, etc

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

> side note on terminals and shells on Windows

> Windows Terminal is quite nice to use

> if everything lives in WSL, i recommend using WSL

> if some project files lives in Windows, i recommend using Powershell.    
> surprisingly a lot of common Linux CLI tools are compiled for Windows too, with package managers like scoop or choco. so its actually quite usable. can be configured to "feel at home" like in Linux    
> Powershell makes it "feel more at home" compared to Command Prompt (cmd), so i recommend Powershell over Command Prompt too. (eg. you can use commands like `ls`)    

> i dont recommend using Cygwin.    
> for "basic" use cases its ok. for more "advanced" things, you start to run into limitations and hacks. you can pretty much achieve whatever you need with either WSL or Powershell

## shared dotfiles

Neovim (btw): https://github.com/gjtiquia/kickstart.nvim

vim (btw): https://github.com/gjtiquia/.vim

lazygit: https://github.com/gjtiquia/lazygit_config

## goals and non-goals

some people like to put all their dotfiles into a single repo

that doesnt work for me, cuz i find that some dotfiles are machine/OS/runtime specific, and some are shared

i prefer a more "modular" approach, where config files are as "self-contained" as possible

this way i can choose individually which dotfiles are "shared", which are not

some people like to use `GNU Stow` for managing their dotfiles

i prefer not to, as i want less dependencies as possible, and a setup that works across Windows, MacOS, and Linux


## setup instructions for $HOME dotfiles



## setup instructions for shared dotfiles
