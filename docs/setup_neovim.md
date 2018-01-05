#  UbuntuでのNeovimのインストールとセットアップ
Ubuntu LTS16.04でneovimのインストールと設定を行った際のメモです

1. [Install](#Install-neovim)
2. [Configure](#Configure)

## Install neovim
[公式のwiki](https://github.com/neovim/neovim/wiki/Installing-Neovim#ubuntu)にあるとおりインストールします

```shell
# インストール
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt-get update
sudo apt-get install neovim
sudo apt-get install python-dev python-pip python3-dev python3-pip
sudo pip2 install --upgrade neovim
sudo pip3 install --upgrade neovim

# vi, vim で neovimが開くように設定
sudo update-alternatives --set vi $(which nvim)
sudo update-alternatives --set vim $(which nvim)
```

インストールが完了したらneovimを起動し、インストールされた内容で問題がないかを確認します。

```
nvim
# 以下neovimのエディタで
:CheckHealth
```

何か問題がある場合には、`CheckHealth`を実行した際に、ErrorやWarningが出ますので、内容を修正する必要があります。
その他に、`init.vim`を修正したり、プラグインの追加などを行ったあとには、`CheckHealth`を実行したほうが良いでしょう。
## Configure
### 設定ファイルのディレクトリ構造
基本的に設定は`~/.config/nvim/`配下に書きます

- .vimrc -> ~/.config/nvim/init.vim
- filetype -> ~/.config/nvim/ftpluin/*.vim
- pluginやその他のvimスクリプト -> ~/.config/nvim/autoload/*.vim

### Install vim-plug

```shell
curl -fLo ~/dotfiles/config/nvim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
