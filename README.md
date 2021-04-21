## Ubuntu Setup

### preparation

-   update packages

```bash
sudo apt-get update
sudo apt upgrade
```

-   install curl and git:

```bash
sudo apt-get install -y build-essential libssl-dev curl file git
```

-   remove unnecessary packages

```bash
sudo apt autoremove
```



### Homebrew

-   install homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

-   Add Homebrew to your PATH in /home/<user>/.profile

```bash
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/<user>/.profile
```



### tools

-   install cli tools

```bash
brew install vim neovim vifm tree bat
```

-   install developing env and tools

```bash
brew install ipython postgresql rabbitmq redis
```

-   install nvm, similar `export` command required if install via `homebrew`

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm install node
```



### Customize shell

-   install zsh and oh-my-zsh

```bash
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

-   install plugins to oh-my-zsh

```bash
brew install autojump 
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
```

-   add plugin settings to `.zshrc` file

```toml
# ~/.zshrc
plugins=(git autojump zsh-autosuggestions zsh-syntax-highlighting git-open)

# autojump
[ -f /home/linuxbrew/.linuxbrew/etc/profile.d/autojump.sh ] && . /home/linuxbrew/.linuxbrew/etc/profile.d/autojump.sh

# set key binding to autocomplete
bindkey ',' autosuggest-accept
```

-   [Powerlevel10k](https://github.com/romkatv/powerlevel10k) color theme

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

-   check current shell and change default shell to zsh, note that this change requires reboot

```bash
echo $SHELL
cat /etc/shells
chsh -s /bin/zsh
```



### customize vim editor

-   install spacevim

```bash
curl -sLf https://spacevim.org/install.sh | bash
pip3 install neovim
```

-   setup wrap in spacevim

```v
# ~/.SpaceVim.d/autoload/custom.vim

func! custom#before() abort
  set wrap
endf
```

-   add setup to spacevim config file

```toml
# ~/.SpaceVim.d/init.toml
[options]
escape_key_binding = 'jj'
bootstrap_before = "custom#before"
autocomplete_method = "deoplete"
# autocomplete_method = 'ycm'
snippet_engine = "ultisnips"
```

-   add language support layer

```toml
# ~/.SpaceVim.d/init.toml

# support for python
[[layers]]
name = "lang#python"
python_interpreter = '/home/linuxbrew/.linuxbrew/bin/python3'
enable_typeinfo = true
python_file_head = [
  '#!/home/linuxbrew/.linuxbrew/bin/python3',
  '# -*- coding: utf-8 -*-',
  '',
  ''
]

[[layers]]
name = "lang#javascript"
auto_fix = true

[[layers]]
name = "format"
format_on_save = true

[[layers]]
name = "checkers"
```

find more setups [here](https://spacevim.org/use-vim-as-ide/)