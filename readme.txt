1. Clone git vim repo anywhere
2. symlink 3 files in cloned vim repo (either lean or vim ) .vimrc.local
.vimrc.bundles.local .vimrc.before.local
in home dir
E.g 
If these files already in home directory delete them
cd ~
ln -s ~/vim/lean/.vimrc.local ~/.vimrc.local
same for other 2. Here vim is cloned in home
Next time just update git repo to sync on all machines

******Steps to get SPF 13 vim distribution working.


Mac
1. Open terminal and run (Enter git username pass if asked or skip)
   curl http://j.mp/spf13-vim3 -L -o - | sh
2. Now in Home folder .spf13-vim3 folder will be created. Hidden files can be seen by cmd + shift + .
   In terminal go to this folder and clone vim settings from GitHub
   	TSHEORAN-M-J2TS:~ tsheoran$ cd .spf13-vim-3/
	TSHEORAN-M-J2TS:.spf13-vim-3 tsheoran$ git clone https://github.com/tejv/vim.git
	Cloning into 'vim'...
	remote: Counting objects: 38, done.
	remote: Compressing objects: 100% (4/4), done.
	remote: Total 38 (delta 0), reused 2 (delta 0), pack-reused 34
	Unpacking objects: 100% (38/38), done.
	TSHEORAN-M-J2TS:.spf13-vim-3 tsheoran$

“”””””””””
3. Now create .vimrc.bundles.local, .vimrc.before.local in Home directory
4. Create symbolic link
       .vimrc.local (already in home directory) to that in vim folder in .spf13 folder
       .vimrc.bundles.local
       .vimrc.before.local

TSHEORAN-M-J2TS:~ tsheoran$ ln -s .vimrc.local .spf13-vim-3/vim/.vimrc.local
ln: .spf13-vim-3/vim/.vimrc.local: File exists
TSHEORAN-M-J2TS:~ tsheoran$ ln -s .vimrc.before.local .spf13-vim-3/vim/.vimrc.before.local
ln: .spf13-vim-3/vim/.vimrc.before.local: File exists
TSHEORAN-M-J2TS:~ tsheoran$ ln -s .vimrc.bundles.local .spf13-vim-3/vim/.vimrc.bundles.local
ln: .spf13-vim-3/vim/.vimrc.bundles.local: File exists
TSHEORAN-M-J2TS:~ tsheoran$ 
“””””””””””””
Step 3 and 4 not working for me.

So do copy of git vim 3 files in HOME directory. If these 3 files already exists delete and then copy.
In future any changes done copy them back to git vim and push to master.
      
5. Install macVim from
   https://github.com/macvim-dev/macvim
6. If it says not from App Store. Go to system preferences -> security-> enable mccvim
7. Open macvim it will be set to spf13. Any changes need to be done only in git vim directory.

8. To open macVim from terminal run this command. Now use gvim to open in terminal.
alias gvim='/Applications/MacVim.app/Contents/MacOS/Vim -g'
  




Windows

1. This folder  has custom vimrc commands which will override or add to spf 13.
2. This folder also has template for various file types.
3. This folder is the one which is needed if vim need to be installed on different pc. 
4. By default HOME dir is C:\users\username\
Any overwritten vimrc should be kept in this folder.
5. But spf 13 keep all its file in HOME\.spf-13 folder. So how it works. By default vim base installation(C:\program files\vim\) looks for any over ride files in HOME dir
HOME dir. 
6. This is achieved by spf 13 using symbolic links. It creates symbolic links of all relavant files in HOME folder to those in spf 13 folder.

******Steps to install vim and spf 13 on new windows pc.
1. Install vim latest version with lua support. One which has in built lua. Lua support is needed if neocomplete plugin need to run. To enable lua support in normal vim
   just copy gvim.exe(with lua), lua.dll and lua folder in original gvim.exe folder. http://www.vim.org/download.php
2. Install Git.   
2. Install spf 13 with steps from webpage(http://vim.spf13.com/) using this option "Installing spf13-vim on Windows
The easiest way is to download and run the spf13-vim-windows-install.cmd file."
3. Copy vim folder(from github repo) in HOME\.spf 13 folder.
4. Now create symlinks by opening command prompt in adminitrative mode. Run below commands. Note change path as per your username. In this case it is teju.

mklink "C:\Users\teju\.vimrc.before.local" "C:\Users\teju\.spf13-vim-3\vim\.vimrc.before.local"
mklink "C:\Users\teju\.vimrc.bundles.local" "C:\Users\teju\.spf13-vim-3\vim\.vimrc.bundles.local"
mklink "C:\Users\teju\.vimrc.local" "C:\Users\teju\.spf13-vim-3\vim\.vimrc.local" 

5. vimrc.before.local runs before spf 13. So it can enable disable stuff(plugin) so that spf 13 found a variable already defined. So it won't use default settings.
6. vimrc.local runs after spf 13 and override spf settings. So we will store our additional commands here.
7. Add new plugins in vimrc.bundles.local file
    e.g
    Bundle \'spf13/vim-colors\'
If a bundle is not needed (completely uninstall) put a comment (") before the line.
After this run     
    vim +BundleInstall! +BundleClean +q
This will add any new plugin and remove commented out plugins.

8. To disable a plugin (not uninstall) 
In vimrc.local file put UnBundle command   
e.g
    UnBundle \'AutoClose\'
Then run below from gvim.
    :BundleClean!
or this from command prompt
    gvim BundleClean!
    
*****Use command prompt to open multiple files silently in vim
Go to the folder where files are in command prompt
cd xxxxxx
then
gvim --remote-silent *.c *.h

******Run Ctags on a folders
Go to the folder where files are in command prompt
cd xxxxxx
then
ctags -R *.*


******Install YouCompleteMe on Windows with clang Working but don't enable clang i.e do not provide ycm_extra_conf file
Follow
https://github.com/Valloric/YouCompleteMe/wiki/Windows-Installation-Guide
Instructions for 64-bit using MinGW64 (clang)

1. Every component used in this tutorial must have same bit architecture. It must be 64 bit.
2. Vim should be 64 bit latest version. https://bintray.com/veegee/generic/vim_x64
3. Install python 2.7 64 bit. Add python.exe path to PATH environement variable.
4. Download libpython‑2.7.10‑cp27‑none‑win_amd64.whl from http://www.lfd.uci.edu/~gohlke/pythonlibs/#libpython
5. Add scripts folder of python install in PATH so that pip exe can run
6. in command prompt go to folder where.whl file was downloaded. 
7. Run 
pip install xxx.whl
This will install libpython27.a
8. Clear previous youcomplete and install new one using
vim +BundleInstall! +BundleClean +q
and disabling youcomplete in vim.before.local
enable again and then run
vim +BundleInstall! +BundleClean +q
again.
9.Install MinGW-w64 http://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/4.8.2/threads-posix/sjlj/
10. Add path of bin to PATH environment variable
11. Download latest clang for 64 bit windows http://llvm.org/releases/download.html#3.3 pre built binaries clang for win 64bit. 
12a. Create a folder ycomp_build in HOME. 
12b. Install clang in ycomp_build\LLVM folder.(means LLVM folder will have bin , include etc directories) Add clang bin path to PATH environment variable. This step is critical
LLVM clang should be installed in build folder.
13. Remember path where LLVM clang installed   %USERPROFILE%\LLVM . Same will be used later in building
14. Install cmake windows  from http://www.cmake.org/download/ and add bin path to PATH environment variable.
15. Replace (userprofile here is HOME)
%USERPROFILE%\.vim\bundle\YouCompleteMe\third_party\ycmd\cpp\BoostParts\boost\detail\interlocked.hpp with that file.https://github.com/Reikion/YouCompleteMe/blob/master/cpp/BoostParts/boost/detail/interlocked.hpp
16. Edit %USERPROFILE%\.vim\bundle\YouCompleteMe\third_party\ycmd\cpp\CMakeLists.txt and add the following lines:
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -include cmath")
add_definitions(-DBOOST_PYTHON_SOURCE)
add_definitions(-DBOOST_THREAD_BUILD_DLL)
add_definitions(-DMS_WIN64)


17. Using command prompt go to ycomp_build dir and run
cmake -G "MinGW Makefiles" -DPATH_TO_LLVM_ROOT=%USERPROFILE%\ycomp_build\LLVM . %USERPROFILE%\.vim\bundle\YouCompleteMe\third_party\ycmd\cpp
18 Run 
mingw32-make ycm_support_libs

19. (Obsolete Do not do this) Copy ycm_core.pyd, ycm_client_support.pyd, and libclang.dll from 
%USERPROFILE%\.vim\bundle\YouCompleteMe\third_party\ycmd to 
%USERPROFILE%\.vim\bundle\YouCompleteMe\python

Over

*****Use youcompleteme for c ,c ++ files
https://wiki.archlinux.org/index.php/YouCompleteMe
http://wiki.yangleo.me/2013/08/15/Let-YCM-Support-C-files.html
