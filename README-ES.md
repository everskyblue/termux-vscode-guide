# Guia De Termux VSCode

guia para instalar vscode en termux

[English - Ingles](https://github.com/everskyblue/termux-vscode-guide/blob/main/README.md)

## Actualizar Termux

suponiendo que a descargado termux en fdroid y le a dado el permiso de almacenamiento ejecute este comando y actualizara los paquetes.

    $ pkg update && pkg upgrade

## Instalación

    $ pkg install tur-repo

una vez instalado tur-repo  procede a descargar code-server

    $ pkg install code-server

esto creara un comando para ejecutar vscode para usarlo desde el navegador tipiando en la terminal **code-server** esto iniciara un servidor local.

pero el abra un error donde no se pueda ejecutar la terminal correctamente.
para eso tenemos hacer un rebuild de la aplicación pero antes vamos a instalar otro paquete zsh.

## Instalar ZSH

instalaremos 

 - git 
 - zsh 
 - oh-my-zsh

usando el comando 

    $ pkg install git zsh

una vez instalado procederemos instalar oh-my-zsh usando curl

    $ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

o clonado el repositorio y ejecutando varios comandos.

    $ git clone https://github.com/matricci/oh-my-zsh-termux
    $ cd oh-my-zsh-termux
    $ ./install.sh


## Editando Configuración

una vez haciendo esta instalacion editaremos **.zshrc** con **nano** que es un editor de terminal 

    $ nano .zshrc

en la primeras lineas se mostrara algo asi

    export PATH=$HOME/bin:/usr/local/bin:$PATH

 nodejs viene instalado cuando instalas code-server
solo hay que añadir la ruta de ubicación donde esta los binarios

    export PATH=$HOME/bin:$HOME/.local/share/pnpm:/usr/local/bin:$PREFIX/opt/nodejs-16/bin:$PATH

guardas el archivo y en la terminal ejecutar otro comando 

    $ source .zshrc

hara los cambios en la terminal o si no terminas el proceso y vuelves a entrar a termux y podrás usar node version 16 y npm version 8

## Activar PNPM O YARN

para activar pnpm o yarn ejecutar cualquiera de estos comandos:

    $ corepack prepare pnpm@latest --activate
    $ corepack prepare yarn@stable --activate

## Rebuild VSCode

por ultimo haremos el rebuild de vscode en la ruta:
	

    $ cd ../usr/lib/code-server/lib/vscode
    $ npm rebuild

esto solucionara los problemas de la terminal en vscode.

### Cambiar Shell

por ultimo detalle para usar zsh ejecuten el comando **chsh** con el valor de **zsh** termine el proceso de termux y vuelva a entrar y tendra zsh

## Configurar Terminal VSCODE

ejecute **code-server** y habra la url dada por code-server.
abra la paleta de comando de vscode y la preferencia e usuario **settings.json** y escriba

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

fin.
