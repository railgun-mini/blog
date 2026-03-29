+++
date = '2026-03-29T04:27:50+08:00'
draft = false
title = 'Git教程'
description = 'Git 技术审计与操作规范'
author = 'railgun'
url = '/hello'
+++

## 1. 核心概念：Git 的“三层楼”
在 Git 中，你的文件处于以下三个状态之一：🚀
1.  **工作区 (Working Directory)**：你正在电脑上修改的文件。
2.  **暂存区 (Staging Area)**：你准备好要提交的文件（像是一个待寄出的快递盒）。
3.  **本地仓库 (Local Repository)**：最终存档的地方，有完整的版本历史。



---

## 2. 基础命令：从零开始

### 第一步：初始化
进入你的项目文件夹，告诉 Git：“从现在起，你归我管了。”
```bash
git init
```

### 第二步：暂存 (Add)
当你改好了一个文件（比如 `index.html`），把它放进“暂存区”：
```bash
git add index.html
# 或者把所有修改过的文件都放进去
git add .
```

### 第三步：提交 (Commit)
把暂存区里的东西正式存入仓库，并写上一段简短的说明（这很重要！）：
```bash
git commit -m "完成了登录页面的布局"
```

---

## 3. 远程协作：连接 GitHub/Gitee
通常我们需要把代码存到云端，以便和他人协作。

* **克隆现有项目**：
    ```bash
    git clone https://github.com/user/repo.git
    ```
* **推送你的代码 (Push)**：
    ```bash
    git push origin main
    ```
* **拉取别人的更新 (Pull)**：
    ```bash
    git pull origin main
    ```

---

## 4. 分支管理：安全的“平行世界”
**分支 (Branch)** 是 Git 最强大的功能。它允许你在不影响主线代码的情况下，开辟一个新战场开发新功能。



* **创建并切换到新分支**：
    ```bash
    git checkout -b feature-login
    ```
* **合并回主分支**：
    先切回主分支：`git checkout main`
    再合并：`git merge feature-login`

---

## 5. 常用避坑命令表

| 命令 | 作用 |
| :--- | :--- |
| `git status` | **最常用！** 查看现在哪些文件被改了，在哪一层。 |
| `git log` | 查看过去的提交历史（翻旧账）。 |
| `git diff` | 查看具体改了哪几行代码。 |
| `git reset --hard` | **慎用！** 强制回滚到之前的某个状态。 |

---

> **💡 小贴士**：刚开始用 Git 可能会觉得命令很难记，这很正常。建议配合带有 GUI 的工具使用，比如 **VS Code 自带的 Git 插件**、**GitHub Desktop** 或者 **Sourcetree**，这样能更直观地看到分支的变化。

**你想让我演示一下如何在具体的项目中（比如 VS Code 里）配置你的 Git 用户名和邮箱吗？**