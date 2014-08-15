## [Help Maintain Vundle](https://github.com/gmarik/Vundle.vim/issues/383)

## About

[Vundle] is short for _Vim bundle_ and is a [Vim] plugin manager.

[Vundle] allows you to...

* keep track of and [configure] your plugins right in the `.vimrc`
* [install] configured plugins (a.k.a. scripts/bundle)
* [update] configured plugins
* [search] by name all available [Vim scripts]
* [clean] unused plugins up
* run the above actions in a *single keypress* with [interactive mode]

[Vundle] automatically...

* manages the [runtime path] of your installed scripts
* regenerates [help tags] after installing and updating

[Vundle] is undergoing an [interface change], please stay up to date to get latest changes.

[![Gitter-chat](https://badges.gitter.im/gmarik/Vundle.vim.png)](https://gitter.im/gmarik/Vundle.vim) for discussion and support.

![Vundle-installer](http://i.imgur.com/Rueh7Cc.png)

## Quick Start

1. Introduction:

   Installation requires [Git] and triggers [`git clone`] for each configured repository to `~/.vim/bundle/` by default.
   Curl is required for search.

   If you are using Windows, go directly to [Windows setup]. If you run into any issues, please consult the [FAQ].
   See [Tips] for some advanced configurations.

2. Set up [Vundle]:

   `$ git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim`

3. Configure Plugins:

   Put this at the top of your `.vimrc` to use Vundle. Remove plugins you don't need, they are for illustration purposes.

   ```vim
set backspace=indent,eol,start
set autowriteall
set number
set hlsearch
set tabstop=4
colorscheme desert "配色方案 "
set background=dark
"set softtabstop=4
set shiftwidth=4
set autoindent
set cindent
set showmatch
set smartindent
set laststatus=2
set ignorecase
set smartcase
set autoread
set incsearch
set fileencodings=utf-8,gbk
set whichwrap=b,s,<,>,[,]  "让退格，空格，上下箭头遇到行首行尾时自动移到下一行（包括insert模式）
"插入模式下移动
"inoremap <c-j> <down>
"inoremap <c-k> <up>
"inoremap <c-l> <right>
"inoremap <c-h> <left>
"===================================================
"修改leader键为逗号
let mapleader=","
"tab切换
nnoremap <leader>t gt
nnoremap <leader>r gT
"使用<leader>空格来取消搜索高亮
nnoremap <leader><space> :noh<cr>
"html中的js加注释 取消注释
nmap <leader>h I//jj
nmap <leader>ch ^xx
nmap <silent> <leader>t :NERDTree<cr>
"快捷键添加"
map \\ :FufCoverageFile<cr>
let g:fuf_coveragefile_globPatterns=['**/*.erb','**/*.rb','**/*.yml']
map <F9> :NERDTree<CR>
" 命令行下按tab键自动完成
 set wildmode=list:full
 set wildmenu
imap jj <esc>
imap kk <esc>:w!

colorscheme desert
set foldmethod=manual
"powerline{
set guifont=PowerlineSymbols\ for\ Powerline
set t_Co=256
let g:Powerline_symbols = 'fancy'
"}
"vundle{
filetype off        " required!
set rtp+=~/.vim/bundle/vundle/
call vundle#rc()
" let Vundle manage Vundle
" required!
Bundle 'gmarik/vundle'
nmap <F8> :TagbarToggle<CR>
"使用<leader>空格来取消搜索高亮
nnoremap <leader><space> :noh<cr>
set wildignore+=*.so,*.swp,*.zip,*/.svn/*

"ycm{"
let g:ctrlp_working_path_mode = 'rw'
let g:ycm_semantic_triggers =  {
  		\   'c' : ['->', '.'],
			\   'objc' : ['->', '.'],
			\   'cpp,objcpp' : ['->', '.', '::'],
			\   'perl' : ['->'],
			\   'php' : ['->', '::'],
			\   'cs,java,javascript,d,vim,ruby,python,perl6,scala,vb,elixir,go' : ['.'],
			\   'lua' : ['.', ':'],
			\   'erlang' : [':'],
			\ }
let g:ycm_filetype_blacklist = {
			\ 'notes' : 1,
			\ 'markdown' : 1,
			\ 'text' : 1,
			\}
let g:ycm_key_list_select_completion = ['<TAB>', '<Down>','<Enter>']
let g:ycm_min_num_of_chars_for_completion = 1
let g:ycm_confirm_extra_conf = 0
"}

"#相较于Command-T等查找文件的插件，ctrlp.vim最大的好处在于没有依赖，干净利落
Bundle 'kien/ctrlp.vim'
"#在输入()，""等需要配对的符号时，自动帮你补全剩余半个
Bundle 'AutoClose'
"#神级插件，ZenCoding可以让你以一种神奇而无比爽快的感觉写HTML、CSS
"Bundle 'ZenCoding.vim'
"#在()、""、甚至HTML标签之间快速跳转；
Bundle 'matchit.zip'
"#显示行末的空格；
Bundle 'ShowTrailingWhitespace'
"#JS代码格式化插件；
Bundle '_jsbeautify'
"#用全新的方式在文档中高效的移动光标，革命性的突破
Bundle 'EasyMotion'
let g:EasyMotion_leader_key = '<Leader><Leader>'
let g:EasyMotion_keys = 'abcdefghijklmnopqrstuvwxyz'
let g:EasyMotion_grouping = '2'
"#自动识别文件编码；
Bundle 'FencView.vim'
"#必不可少，在VIM的编辑窗口树状显示文件目录
Bundle 'The-NERD-tree'
"#NERD出品的快速给代码加注释插件，选中，`ctrl+h`即可注释多种语言代码；
Bundle 'The-NERD-Commenter'
let NERDShutUp=1
"支持单行和多行的选择，//格式
map <c-h> ,c<space>
"#解放生产力的神器，简单配置，就可以按照自己的风格快速输入大段代码。
Bundle 'UltiSnips'
let g:UltiSnipsExpandTrigger="<c-j>"
let g:UltiSnipsJumpForwardTrigger="<c-j>"
let g:UltiSnipsJumpBackwardTrigger="<c-k>"
"#让代码更加易于纵向排版，以=或,符号对齐
Bundle 'Tabular'
"#迄今位置最好的自动VIM自动补全插件了吧
"#Vundle的这个写法，是直接取该插件在Github上的repo
"Bundle 'Valloric/YouCompleteMe'
Bundle 'Lokaltog/vim-powerline'
Bundle 'majutsushi/tagbar'
"Bundle 'scrooloose/syntastic'
Bundle 'vim-scripts/VisIncr'
Bundle 'tpope/vim-rails'
Bundle 'othree/xml.vim'
Bundle 'rodjek/vim-puppet'
Bundle 'godlygeek/tabular'
Bundle 'L9'
Bundle 'FuzzyFinder'
Bundle 'scrooloose/nerdtree'

Bundle "MarcWeber/vim-addon-mw-utils"
Bundle "tomtom/tlib_vim"
Bundle "garbas/vim-snipmate"
Bundle "honza/vim-snippets"
Bundle "jQuery"
Bundle 'JavaScript-syntax'
Bundle 'othree/html5.vim'
Bundle 'groenewege/vim-less'
Bundle 'Markdown'
Bundle 'Markdown-syntax'
Bundle 'winmanager'
Bundle 'scrooloose/nerdcommenter'
Bundle 'taglist.vim'
Bundle 'fholgado/minibufexpl.vim'
"Bundle 'spf13/snipmate-snippets'
Bundle 'pangloss/vim-javascript'
Bundle 'mattn/emmet-vim'
"放置在Bundle的设置后，防止意外BUG"
filetype plugin indent on
syntax on
function! TwoSpace()
	setlocal tabstop=2
  setlocal shiftwidth=2
endfunction
au FileType ruby call TwoSpace()
au FileType coffee call TwoSpace()
au FileType vim call TwoSpace()
au FileType eruby call TwoSpace()
" HAML hax {{{
" Haml likes indents of 2 spaces, just like our ruby.
au FileType haml call TwoSpace()
" }}}
   ```

4. Install Plugins:

   Launch `vim` and run `:PluginInstall`

   To install from command line: `vim +PluginInstall +qall`

## Docs

See the [`:h vundle`](https://github.com/gmarik/Vundle.vim/blob/master/doc/vundle.txt) Vimdoc for more details.

## Changelog

See the [changelog](https://github.com/gmarik/Vundle.vim/blob/master/changelog.md).

## People Using Vundle

see [Examples](https://github.com/gmarik/Vundle.vim/wiki/Examples)

## Contributors

see [Vundle contributors](https://github.com/gmarik/Vundle.vim/graphs/contributors)

*Thank you!*

## Inspiration & Ideas

* [pathogen.vim](http://github.com/tpope/vim-pathogen/)
* [Bundler](https://github.com/bundler/bundler)
* [Scott Bronson](http://github.com/bronson)

## Also

* Vundle was developed and tested with [Vim] 7.3 on OS X, Linux and Windows
* Vundle tries to be as [KISS](http://en.wikipedia.org/wiki/KISS_principle) as possible

## TODO:
[Vundle] is a work in progress, so any ideas and patches are appreciated.

* ✓ activate newly added bundles on `.vimrc` reload or after `:PluginInstall`
* ✓ use preview window for search results
* ✓ Vim documentation
* ✓ put Vundle in `bundles/` too (will fix Vundle help)
* ✓ tests
* ✓ improve error handling
* allow specifying revision/version?
* handle dependencies
* show description in search results
* search by description as well
* make it rock!

[Vundle]:http://github.com/gmarik/Vundle.vim
[Windows setup]:https://github.com/gmarik/Vundle.vim/wiki/Vundle-for-Windows
[FAQ]:https://github.com/gmarik/Vundle.vim/wiki
[Tips]:https://github.com/gmarik/Vundle.vim/wiki/Tips-and-Tricks
[Vim]:http://www.vim.org
[Git]:http://git-scm.com
[`git clone`]:http://gitref.org/creating/#clone

[Vim scripts]:http://vim-scripts.org/vim/scripts.html
[help tags]:http://vimdoc.sourceforge.net/htmldoc/helphelp.html#:helptags
[runtime path]:http://vimdoc.sourceforge.net/htmldoc/options.html#%27runtimepath%27

[configure]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L126-L233
[install]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L234-L254
[update]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L255-L265
[search]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L266-L295
[clean]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L303-L318
[interactive mode]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L319-L360
[interface change]:https://github.com/gmarik/Vundle.vim/blob/v0.10.2/doc/vundle.txt#L372-L396
