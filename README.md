## 下载并源码编译安装vim
由于apt安装源安装的vim并不支持python、lua等插件，所有需要下载vim源码编译安装以支持

```shell
git clone https://github.com/vim/vim.git
cd vim
git checkout -b v8.1.1564 8.1.1564
sudo apt install python-dev python3-dev ruby-dev lua5.1 lua5.1-dev libncurses5-dev libperl-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev
./configure --with-features=huge --enable-pythoninterp --enable-rubyinterp --enable-luainterp --enable-perlinterp --with-python-config-dir=/usr/lib/python2.7/config/ --enable-gui=gtk2 --enable-cscope --prefix=/usr
make
make install
```
其中，--enable-pythoninterp、--enable-rubyinterp、--enable-perlinterp、--enable-luainterp 等分别表示支持 ruby、python、perl、lua 编写的插件，--enable-gui=gtk2 表示生成采用 GNOME2 风格的 gvim，--enable-cscope 支持 cscope，--with-python-config-dir=/usr/lib/python2.7/config/ 指定 python 路径（先自行安装 python 的头文件 python-devel），这几个特性非常重要，影响后面各类插件的使用。注意，你得预先安装相关依赖库的头文件，python-devel、python3-devel、ruby-devel、lua-devel、libX11-devel、gtk-devel、gtk2-devel、gtk3-devel、ncurses-devel，如果缺失，源码构建过程虽不会报错，但最终生成的 vim 很可能缺失某些功能。构建完成后在 vim 中执行
```shell
:echo has('python')
```
若输出 1 则表示构建出的 vim 已支持 python，反之，0 则不支持。

## 安装bundle插件
```shell
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
## 插件管理
插件安装
```shell
:PluginInstall
```
要卸载插件，先在 .vimrc 中注释或者删除对应插件配置信息，然后在 vim 中执行
```shell
:PluginClean
```
即可删除对应插件。插件更新频率较高，差不多每隔一个月你应该看看哪些插件有推出新版本，批量更新，只需执行
```shell
:PluginUpdate
```

## 安装YouComplete插件
```shell
cd ~/.vim/bundle/YouCompleteMe
./install.py --gocode-completer --clang-completer --go-completer
```
