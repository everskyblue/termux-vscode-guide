# Termux VSCode Guide

guide to install vscode in termux

[Spanish - Español](https://github.com/everskyblue/termux-vscode-guide/blob/main/README-ES.md)

## Update Termux

Assuming you have downloaded termux on fdroid and given the storage permission run this command and it will update the packages.

     $ pkg update && pkg upgrade

## Facility

     $ pkg install tur-repo

once tur-repo is installed proceed to download code-server

     $ pkg install code-server

This will create a command to run vscode to use from the browser by typing in the terminal **code-server** this will start a local server.

but the open an error where it can't run the terminal correctly.
For that we have to rebuild the application but first we are going to install another zsh package.

## Install ZSH

we will install

  - git
  - zsh
  - oh-my-zsh

using the command

     $ pkg install git zsh

once installed we will proceed to install oh-my-zsh using curl

     $ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

or cloned the repository and running various commands.

     $ git clone https://github.com/matricci/oh-my-zsh-termux
     $ cd oh-my-zsh-termux
     $ ./install.sh


## Editing Configuration

once doing this installation we will edit **.zshrc** with **nano** which is a terminal editor

     $ nano .zshrc

in the first lines it will show something like this

     export PATH=$HOME/bin:/usr/local/bin:$PATH

  nodejs comes installed when you install code-server
you just have to add the location path where the binaries are

     export PATH=$HOME/bin:$HOME/.local/share/pnpm:/usr/local/bin:$PREFIX/opt/nodejs-16/bin:$PATH

save the file and in the terminal run another command

     $ source .zshrc

It will make the changes in the terminal or if it does not finish the process and go back to termux and you can use node version 16 and npm version 8

## Enable PNPM OR YARN

To activate pnpm or yarn run any of these commands:

     $ corepack prepare pnpm@latest --activate
     $ corepack prepare yarn@stable --activate

## Rebuild VSCode

Finally we will do the rebuild of vscode in the route:


     $ cd ../usr/lib/code-server/lib/vscode
     $ npm rebuild

This will fix terminal issues in vscode.

### Change Shell

Lastly, to use zsh, execute the command **chsh** with the value of **zsh**, finish the termux process and log in again and you will have zsh

## Set Terminal VSCODE

run **code-server** and there will be the url given by code-server.
open vscode command palette and user preference **settings.json** and type

```json
{
   "terminal.integrated.profiles.linux":{
     "bash":{
       "path":"bash",
       "icon":"terminal-bash"
     },
     "zsh":{
       "path":"zsh"
     },
     "fish":{
       "path":"fish"
     },
     "tmux":{
       "path":"tmux",
       "icon":"terminal-tmux"
     },
     "pwsh":{
       "path":"pwsh",
       "icon":"terminal-powershell"
     },
     "shellTermux":{
       "path":"${env:$HOME}/.termux/shell"
     }
   },
   "terminal.integrated.defaultProfile.linux":"zsh"
}
```

end.
