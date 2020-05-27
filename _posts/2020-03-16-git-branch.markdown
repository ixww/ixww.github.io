---
layout:     post
title:      "mac终端显示git分支"
subtitle:   "mac终端显示git分支"
date:       2020-03-16
author:     "iXww"
tags:
    - git
---

当我第一次在mac系统下使用git的时候，发现一个问题，git默认是不显示当前所在的分支名称，然后网上查找资料，找到了解决办法，终于可以显示本地当前分支，现在分享如下。  

1.  进入home目录：  
cd ~  
2. 编辑.bashrc文件(mac下编辑.bash_profile)  
vi .bashrc  
3. 将下面的代码加入到文件的最后处  
```
function git_branch {
  branch="`git branch 2>/dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
  if [ "${branch}" != "" ];then
      if [ "${branch}" = "(no branch)" ];then
          branch="(`git rev-parse --short HEAD`...)"
      fi
      echo " ($branch)"
  fi
}
export PS1='\u@\h \[\033[01;36m\]\W\[\033[01;32m\]$(git_branch)\[\033[00m\] \$ '
```
4. 保存退出  
5. 执行加载命令(mac下还是操作.bash_profile文件)  
source ./.bashrc  
6. 完成  
Mac 下面启动的 shell 是 login shell，所以加载的配置文件是.bash_profile，不会加载.bashrc。如果你是 Mac 用户的话，需要再执行下面的命令，这样每次开机后才会自动生效：  
echo "[ -r ~/.bashrc ] && source ~/.bashrc" >> .bash_profile  