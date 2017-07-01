---
title: 终于开始使用Vim开发
date: 2017-07-01 15:38:20
tags: 
- vim
- linux
categories: 
- 技术博文
---

大二就接触了Vim，那会儿刚会用最常见的指令操作vim，就已经被深深吸引：这才是编程的正确姿势，鼠标什么的给我拿远点。大四在北京一家小公司实习做JAVA测试，公司也是规定用Vim编程（不明白编程工具为什么都要统一？）。当时傻乎乎的，不会用任何插件，跳转补全模板什么的都没有，就是硬生生的手敲代码，愣是敲了几个月时间，敲出了好多没什么技术含量的增删改查(CRUD)代码。

后来参加工作，基本都是在宇宙第一IDE：Visual Studio下开发，觉得特别美好。后来到创业公司用不起Windows了，换成了Ubuntu系统，一直在Eclipse下开发，但总是觉得舒服，不满意Eclispe的速度，构建不够自动化也是我吐槽的地方。

<!-- more -->

自己多次尝试将coding平台转到Vim下面，但屡屡尝试却屡屡失败，最后都重新投入到IDE的怀抱。每次都给自己找很多借口，调试不方便，补全不方便，函数变量跳转不方便等等，最后的妥协的方式就是给IDE安装了具有vim主要特性的插件，hjkl/yy/gg/dd等命令都可以使用，还可以使用IDE的功能，但心理也一直有抛弃IDE的情结。

这次彻底说服了自己，公司的项目也开始使用Cmake构建，我就可以完全使用了Vim进行开发，gbd调试。经过了一小段时间的磨合，基本接受了这套工具。甚至有时给我带来惊喜感叹道：这功能太NB了。

都说Vim上手难，其实我觉得上手编简单的程序其实很简单，走一遍vimtutor基本就可以当高级记事本用了，平常写些小程序刷刷Leetcode足够了。难是难在真正在工作中，想将Vim中当做生产力工具，需要经过繁琐的配置和摸索。每一个IDE里理所当然的功能，在Vim里都需要固定的一个或者几个插件配合完成才可以，这正好契合Unix/Linux“小而美”的哲学。

Vim的插件多如牛毛，每一个功能都有好几个工具可供选择，折腾起来实在太费事。幸运的是开源有人开源了一套很好的配置[spf13-vim](https://github.com/spf13/spf13-vim)，常用插件基本都包含了，模块划分清楚，配置简单，快捷键设置合理。这套配置是vimer的大礼包，再也不用纠结到底用哪一个插件如何配置了，因为有大神已经帮我们把坑都踩过了，告诉我们：顺着这条路走就行。

有几个插件我觉得是神器：undotree, vim-easymotion, vim-fugitive, ultisnips+vim-snipptes, YouCompleteMe，再加上buffer，nerdtree，tagbar等插件工具，基本就满足了我平常的开发。要说和IDE哪个效率高，老实说：差不多。都只是工具，大家要实现的功能也都一样，又能有多大差别呢？无非就是使用Vim姿势比较好看，或者说格调高一些？就像两个人吃饭，一个用筷子吃，一个手抓着吃，其实他俩最后能吃多少，和用什么吃基本没什么关系，还是取决于每个人的饭量（实力）。无非就是用筷子吃吃的文雅一些罢了。

我都工作三年了，还在折腾这些工具，好像很没有前途的样子，我应该写改变世界的软件啊，把别人制造出来的工具用熟练有什么好炫耀的。但其实程序员的生活都是很具体的，魔鬼都在细节中。如果每天都要使用的工具自己都觉得不舒服，而且没法给它折腾舒服，又怎么指望他能写出很牛的软件呢？我不相信Linus是用记事本写出来的Linux内核。现在使用的spf13-vim的作者Steve Francia，也是Google的Go语言的作者。他开源的这套Vim配置，肯定也是平常工作中不断折腾，精心打磨的结果。而且我敢肯定他折腾的时间肯定比我多很多，但一样不耽误他写改变世界的软件。

所以，把工具打磨顺手，多花一些时间也不过分。这体现了一个程序员有没有geek的精神：如果觉得一个东西不爽，那就自己动手把它改造成爽的样子。

最后附上我目前使用的vim插件。

``` vim
" My Plugins
Plugin 'gmarik/vundle'
Plugin 'MarcWeber/vim-addon-mw-utils'
Plugin 'tomtom/tlib_vim'
Plugin 'mileszs/ack.vim'
Plugin 'scrooloose/nerdtree'
Plugin 'altercation/vim-colors-solarized'
Plugin 'spf13/vim-colors'
Plugin 'tpope/vim-surround'
Plugin 'tpope/vim-repeat'
Plugin 'rhysd/conflict-marker.vim'
Plugin 'jiangmiao/auto-pairs'
Plugin 'ctrlpvim/ctrlp.vim'
Plugin 'tacahiroy/ctrlp-funky'
Plugin 'terryma/vim-multiple-cursors'
Plugin 'vim-scripts/sessionman.vim'
Plugin 'matchit.zip'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
Plugin 'powerline/fonts'
Plugin 'bling/vim-bufferline'
Plugin 'easymotion/vim-easymotion'
Plugin 'jistr/vim-nerdtree-tabs'
Plugin 'flazz/vim-colorschemes'
Plugin 'mbbill/undotree'
Plugin 'nathanaelkane/vim-indent-guides'
Plugin 'vim-scripts/restore_view.vim'
Plugin 'mhinz/vim-signify'
Plugin 'tpope/vim-abolish.git'
Plugin 'osyo-manga/vim-over'
Plugin 'kana/vim-textobj-user'
Plugin 'kana/vim-textobj-indent'
Plugin 'gcmt/wildfire.vim'
Plugin 'scrooloose/syntastic'
Plugin 'tpope/vim-fugitive'
Plugin 'mattn/webapi-vim'
Plugin 'mattn/gist-vim'
Plugin 'scrooloose/nerdcommenter'
Plugin 'tpope/vim-commentary'
Plugin 'godlygeek/tabular'
Plugin 'luochen1990/rainbow'
Plugin 'majutsushi/tagbar'
Plugin 'Valloric/YouCompleteMe'
Plugin 'SirVer/ultisnips'
Plugin 'honza/vim-snippets'
Plugin 'klen/python-mode'
Plugin 'yssource/python.vim'
Plugin 'python_match.vim'
Plugin 'pythoncomplete'
Plugin 'rust-lang/rust.vim'
Plugin 'tpope/vim-markdown'
Plugin 'spf13/vim-preview'
Plugin 'tpope/vim-cucumber'
Plugin 'cespare/vim-toml'
Plugin 'quentindecock/vim-cucumber-align-pipes'
Plugin 'saltstack/salt-vim'
Plugin 'vim-scripts/fcitx.vim'
Plugin 'derekwyatt/vim-fswitch'
Plugin 'octol/vim-cpp-enhanced-highlight'
Plugin 'sukima/xmledit'
Plugin 'rdnetto/YCM-Generator'
Plugin 'myusuf3/numbers.vim'
Plugin 'vim-scripts/DoxygenToolkit.vim'

```



