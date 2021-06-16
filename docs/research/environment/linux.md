---
layout: default
title: Linux
parent: Environment
grand_parent: Research
---

# Linux
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## /etc/inputrc

### turn off the bell

```
sudo vim /etc/inputrc
```

uncomment following line and save

```
set bell-style none
```

source change by reopening sesstion

## vim

### download neovim

download appimage from [here](https://github.com/neovim/neovim/releases)

```
wget https://github.com/neovim/neovim/releases/download/nightly/nvim.appimage
chmod u+x nvim.appimage
```

nightly version is required for plugging in telescope

### ~/.bashrc

In order to open neovim with vim command, add the following line in ~/.bashrc

```
alias vim='~/nvim.appimage'
```

source change by following command

```
source .bashrc
```

now vim command will open nvim

### basic configuration

neovim is configured by ~/.config/nvim/init.vim file

```
set guicursor=
set rnu
set nu
set nohlsearch
set hidden
set noerrorbells
set tabstop=4 softtabstop=4
set shiftwidth=4
set expandtab
set smartindent
set nowrap
set noswapfile
set nobackup
set undodir=~/.vim/undodir
set undofile
set incsearch
set scrolloff=8
set signcolumn=yes
set colorcolumn=80

```

### plug-in manager

download [vim-plug](https://github.com/junegunn/vim-plug)

and add following to init.vim

```
call plug#begin('~/.vim/plugged/')

Plug 'gruvbox-community/gruvbox'
Plug 'nvim-lua/popup.nvim'
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'
Plug 'nvim-telescope/telescope-fzy-native.nvim'

call plug#end()

colorscheme gruvbox
set background=dark

let mapleader = " "

" telescope remap
nnoremap <leader>pb :lua require('telescope.builtin').buffers()<CR>
nnoremap <leader>pf :lua require('telescope.builtin').find_files()<CR>
```

type following vim command to download plug-ins

```
:PlugInstall
```

## git

### basic configuration

~/.gitconfig

## tmux


