+++
date = '2026-03-29T04:31:37+08:00'
draft = false
title = 'Git 技术审计与操作规范'
description = 'Git 技术审计与操作规范'
author = 'railgun'
url = '/hea'
+++

## 1.用户

```bash
# 查看用户名 ：
git config user.name

# 查看密码： 
git config user.password

# 查看邮箱：
git config user.email

# 查看配置信息： 
git config --list  

# 修改用户名：
git config --global user.name "xxxx(新的用户名)"
# 清除用户名
git config --global --unset user.name

# 修改密码：
git config --global user.password "xxxx(新的密码)"

# 修改邮箱：
git config --global user.email "xxxx@xxx.com(新的邮箱)"


git config --global --replace-all user.name "你的 git 的名称"

git config --global --replace-all uesr.email "你的 git 的邮箱"
# 将所有 github.com 的 HTTPS 请求转为 SSH 
git config --global url."git@github.com:".insteadOf "https://github.com/"
# 删除配置
git config --global --unset "url.git@github.com:.insteadOf"
```

2.项目

``` shell
# 克隆项目
git clone xxx

# 会添加当前目录下所有更改到暂存区，包括你可能不想提交的文件。
git add . 

# 用于提交当前分支上所有已跟踪文件的更改到本地仓库。这里的 -a 选项告诉 Git 自动暂存（stage）所有已修改或已删除的文件到暂存区（staging area），然后进行提交。但是，这个命令不会自动暂存新创建的文件，这些文件需要手动添加到暂存区。
git commit -a "bastic mode"
# -a：这个选项是 --all 的简写，它指示 Git 包括所有已修改（modified）、已删除（deleted）的文件到提交中。请注意，这个选项不会包括未跟踪（untracked）的文件，即那些之前从未被 Git 跟踪的文件。
# "bastic mode"：这是提交信息（commit message），用于描述提交所做的更改。在本例中，提交信息是 "bastic mode"。

# 用于将本地仓库的更改推送到远程仓库。
git push

# 查看提交历史
git log
```
