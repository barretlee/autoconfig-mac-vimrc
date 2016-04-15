# autoconfig-mac-vimrc

I'm a front-end engineer, and also a vimer, maybe the config file is suitable for you. This file did lots of things, such as:

- install brew if not exist.
- install fonts
- install colorschemes
- install ack 
- install all listed bundle plugins, if exist, try update.
- install YouComplete for nodejs
- and so on.

![pic](http://ww3.sinaimg.cn/large/6c0378f8gw1f2vlasl7e5j21kw0zkanh.jpg)

The `<leader>` key is `,`，use `,ne` open folders.

## Install 

The first approach:

- copy the bash code at the bottom to `install.sh`
- run command `chmod +x install.sh`
- run command `./install.sh`

The second approach:

```bash
git clone https://github.com/barretlee/autoconfig-mac-vimrc.git;
cd autoconfig-mac-vimrc;
chmod +x install;
./install;
```

__Attention:__ This shell script contains lots of plugins and tools, if you have never installed, it may takes a little long time, about 15+ mins in good network.

__bash code__
```bash
#!/bin/bash
# @author Barret Lee<barret.china@gmail.com>

[[ -d ~/.vim ]] || mkdir ~/.vim;

# tmp dir
[[ -d ~/v-tmp ]] || mkdir ~/v-tmp;

# .vimrc
cd ~/v-tmp;
[[ -d ~/v-tmp/rc ]] || git clone https://github.com/barretlee/autoconfig-mac-vimrc.git;

# backup origin vimrc file
[[ -f ~/.vimrc-bak ]] || cp ~/.vimrc ~/.vimrc-bak;
mv ~/v-tmp/autoconfig-mac-vimrc/.vimrc ~/.vimrc;
[[ -d ~/.vim/bundle/Vundle.vim ]] || git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim;

# colors schemes
cd ~/v-tmp;
[[ -d ~/v-tmp/vim-colorschemes ]] || git clone https://github.com/flazz/vim-colorschemes.git;
[[ -d ~/.vim/colors ]] || mv ~/v-tmp/vim-colorschemes/colors ~/.vim/;

# fonts for airline
cd  ~/v-tmp;
[[ -d ~/v-tmp/fonts ]] || git clone https://github.com/powerline/fonts.git;
cd fonts;
sh ./install.sh;

if type brew > /dev/null; then
  echo "Homebrew Exists";
else
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)";
fi;

# ack supported
brew install ack ag;

# YouCompleteMe supported
if [[ -d ~/.vim/bundle/YouCompleteMe ]]; then
  echo "YouCompleteMe Exists";
else
  git clone https://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle/YouCompleteMe;
  cd ~/.vim/bundle/YouCompleteMe;
  # for nodejs
  ./install.py --tern-completer;
fi;

# update vim, replace the origin 
# brew install vim --override-system-vi --with-lua --HEAD;

# install vim plugins
vim +PluginInstall! +qall;

# rm tmp dir
# rm -rf ~/v-tmp;
echo "You can remove the temporary directory ~/v-tmp";
```

## Thanks & LICENSE

Thanks for @noscripter.

MIT LICENSE.

