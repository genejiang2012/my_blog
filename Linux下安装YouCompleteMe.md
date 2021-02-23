# Linux下安装YouCompleteMe

[TOC]

## CentOS

### 查看环境

1. 查看Linux版本

   ```
   [root@iZbp17x826kn36gp8wscduZ ~]# uname -a
   Linux iZbp17x826kn36gp8wscduZ 3.10.0-1127.13.1.el7.x86_64 #1 SMP Tue Jun 23 15:46:38 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
   ```

2. 查看python版本

   ```
   [root@iZbp17x826kn36gp8wscduZ ~]# python3 --version
   Python 3.6.8
   ```

3. 查看vim版本

   ```
   [root@iZbp17x826kn36gp8wscduZ ~]# vim --version
   VIM - Vi IMproved 8.2 (2019 Dec 12, compiled Feb 22 2021 17:50:09)
   Included patches: 1-2531
   Compiled by genejiang2012@outlook.com
   Huge version without GUI.  Features included (+) or not (-):
   +acl               -farsi             +mouse_sgr         +tag_binary
   +arabic            +file_in_path      -mouse_sysmouse    -tag_old_static
   +autocmd           +find_in_path      +mouse_urxvt       -tag_any_white
   +autochdir         +float             +mouse_xterm       -tcl
   -autoservername    +folding           +multi_byte        +termguicolors
   -balloon_eval      -footer            +multi_lang        +terminal
   +balloon_eval_term +fork()            -mzscheme          +terminfo
   -browse            +gettext           -netbeans_intg     +termresponse
   ++builtin_terms    -hangul_input      +num64             +textobjects
   +byte_offset       +iconv             +packages          +textprop
   +channel           +insert_expand     +path_extra        +timers
   +cindent           +ipv6              -perl              +title
   -clientserver      +job               +persistent_undo   -toolbar
   -clipboard         +jumplist          +popupwin          +user_commands
   +cmdline_compl     +keymap            +postscript        +vartabs
   +cmdline_hist      +lambda            +printer           +vertsplit
   +cmdline_info      +langmap           +profile           +virtualedit
   +comments          +libcall           -python            +visual
   +conceal           +linebreak         +python3/dyn       +visualextra
   +cryptv            +lispindent        +quickfix          +viminfo
   +cscope            +listcmds          +reltime           +vreplace
   +cursorbind        +localmap          +rightleft         +wildignore
   +cursorshape       -lua               +ruby/dyn          +wildmenu
   +dialog_con        +menu              +scrollbind        +windows
   +diff              +mksession         +signs             +writebackup
   +digraphs          +modify_fname      +smartindent       -X11
   -dnd               +mouse             -sound             -xfontset
   -ebcdic            -mouseshape        +spell             -xim
   +emacs_tags        +mouse_dec         +startuptime       -xpm
   +eval              -mouse_gpm         +statusline        -xsmp
   +ex_extra          -mouse_jsbterm     -sun_workshop      -xterm_clipboard
   +extra_search      +mouse_netterm     +syntax            -xterm_save
      system vimrc file: "$VIM/vimrc"
        user vimrc file: "$HOME/.vimrc"
    2nd user vimrc file: "~/.vim/vimrc"
         user exrc file: "$HOME/.exrc"
          defaults file: "$VIMRUNTIME/defaults.vim"
     fall-back for $VIM: "/usr/local/share/vim"
   Compilation: gcc -std=gnu99 -c -I. -Iproto -DHAVE_CONFIG_H -g -O2 -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=1 
   Linking: gcc -std=gnu99 -L. -Wl,-z,relro -fstack-protector -rdynamic -Wl,-export-dynamic -L/usr/local/lib -Wl,--as-needed -o vim -lm -ltinfo -ldl 
   ```
### 安装依赖库
```
 yum install python-devel
 yum install libffi-devel -y
 yum install libclang-dev
 yum install cmake
```
### 更新GCC

1. 安装centos-release-scl

   ```
   yum install centos-release-scl
   ```

   

2. 安装devtoolset，注意，如果想安装7.*版本的，就改成devtoolset-9-gcc*，以此类推

   ```
   yum install devtoolset-9-gcc*
   ```

   

3. 激活对应的devtoolset，所以你可以一次安装多个版本的devtoolset，需要的时候用下面这条命令切换到对应的版本

   ```
   scl enable devtoolset-8 bash
   ```
    补充：这条激活命令只对本次会话有效，重启会话后还是会变回原来的4.8.5版本，要想随意切换可按如下操作。

    首先，安装的devtoolset是在 /opt/rh 目录下的，如图
   ```
   [root@iZbp17x826kn36gp8wscduZ bin]# cd /opt/rh
   [root@iZbp17x826kn36gp8wscduZ rh]# ll
   total 4
   dr-xr-xr-x 3 root root 4096 Feb 23 14:58 devtoolset-9
   [root@iZbp17x826kn36gp8wscduZ rh]# cd devtoolset-9/
   [root@iZbp17x826kn36gp8wscduZ devtoolset-9]# ll
   total 8
   -rwxr-xr-x  1 root root 1048 May 27  2020 enable
   dr-xr-xr-x 17 root root 4096 Feb 23 14:58 root
   ```

   启动版本, 

   ```
   source ./enable
   ```

   

4. 查看GCC版本

    ```
    gcc -v
    ```
5. 替换旧的GCC

   ```
   mv /usr/bin/gcc /usr/bin/gcc-4.8.5
   
   ln -s /opt/rh/devtoolset-9/root/bin/gcc /usr/bin/gcc
   
   mv /usr/bin/g++ /usr/bin/g++-4.8.5
   
   ln -s /opt/rh/devtoolset-9/root/bin/g++ /usr/bin/g++
   ```

   

### 下载并安装YouCompleteMe

```
git clone https://github.com/Valloric/YouCompleteMe.git
cd YouCompleteMe
git submodule update --init --recursive
python3 install.py --clang-completer --system-libclang
```

### 配置vimrc

配置YouCompleteMe

```
let g:ycm_global_ycm_extra_conf = '~/.vim/bundle/YouCompleteMe/third_party/ycmd/examples/.ycm_extra_conf.py'
```





