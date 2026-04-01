+++
date = '2026-03-29T04:27:50+08:00'
draft = false
title = 'Windows Terminal'
description = '终端的配置和美化'
author = 'railgun'
url = '/windows-terminal'
+++
# 一、安装

## 1. WinGet使用教程

```powershell
# 查询
winget search 软件名
# 安装
winget install 软件ID或名称
# 示例：安装 Chrome (推荐使用 ID 以确保准确性)
winget install Google.Chrome
# 常用参数：
# --interactive：弹出安装界面手动点击
# --silent：静默安装（后台自动完成）

winget uninstall 软件名或ID
# 示例：
winget uninstall WhatsApp


# 列出所有有更新的软件
winget upgrade

# 更新指定软件
winget upgrade 软件ID

# 一键更新电脑上所有可更新的软件（神器！）
winget upgrade --all
```

## 2. 安装terminal

```powershell
# 发布者.软件名（精确搜索 ，防止同名）
winget install Microsoft.WindowsTerminal
```

## 3. 设置临时代理

```powershell
$env:http_proxy = "http://127.0.0.1:10808"
$env:https_proxy = "http://127.0.0.1:10808"

# 可以直接在$PROFILE文件中设置函数
function Set-Proxy {
    $env:http_proxy  = "http://127.0.0.1:10808"
    $env:https_proxy = "http://127.0.0.1:10808"
    # 可选：有些工具也认 ALL_PROXY 或 no_proxy，按需添加
    # $env:ALL_PROXY = "http://127.0.0.1:10808"
    Write-Host "✅ HTTP/HTTPS proxy set to http://127.0.0.1:10808" -ForegroundColor Green
}

function Clear-Proxy {
    if (Test-Path Env:\http_proxy)  { Remove-Item Env:\http_proxy }
    if (Test-Path Env:\https_proxy) { Remove-Item Env:\https_proxy }
    # 如果设置了 ALL_PROXY，也可以一并清除
    # if (Test-Path Env:\ALL_PROXY) { Remove-Item Env:\ALL_PROXY }
    Write-Host "🧹 HTTP/HTTPS proxy cleared." -ForegroundColor Yellow
}

# 允许本地脚本运行（以普通用户身份打开 PowerShell）
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

# 二、美化终端

## 1. 安装Nerd Fonts字体

[Nerd Fonts 官网](https://www.nerdfonts.com/font-downloads)下载，JetBrainsMono Nerd Font

## 2. 配置Oh My Posh

- 安装Oh My Posh
```powershell
# -s 指定安装源为winget
winget install JanDeDobbeleer.OhMyPosh -s winget

# 检查 profile 文件是否存在
# 在 PowerShell 中，$PROFILE 是一个自动变量，它指向当前用户、当前主机（如 PowerShell 控制台或 PowerShell ISE）所使用的配置脚本（profile script）的路径。这个脚本会在每次启动 PowerShell 时自动运行（如果文件存在的话）。
Test-Path $PROFILE

# 如果不存在，可以创建profile
New-Item -Path $PROFILE -Type File -Force

notepad.exe $PROFILE
oh-my-posh init pwsh --config "pure" | Invoke-Expression
```

- 修改PowerShell 的个性化配置文件
```powershell
# 记事本打开 $PROFILE就是C:\Users\你的用户名\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
notepad.exe $PROFILE
# 文件中添加 oh-my-posh init pwsh --config "xxxx" | Invoke-Expression
```

## 3. 配置starship（替换oh my posh）

- 安装scoop命令行包管理器
```powershell
# 可以通过scoop安装starship也可以轻量美化
# irm(Invoke-RestMethod)  PowerShell 中用于发送 HTTP/HTTPS 请求并自动处理响应内容的内置 cmdlet
# iex(Invoke-Expression)  PowerShell 中用于执行脚本
irm get.scoop.sh | iex

# 卸载scoop
scoop uninstall *
Remove-Item -Recurse -Force "$env:USERPROFILE\scoop"
```

- 通过scoop安装starship
```powershell
# 安装starship
scoop install starship
```

# 三、终端配置

打开终端json配置文件，修改为下json（可以自定义一些喜欢的配置）

```json
{
    "$help": "https://aka.ms/terminal-documentation",
    "$schema": "https://aka.ms/terminal-profiles-schema",
    "actions": [],
    "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
    "centerOnLaunch": true, // 关键行：启动时自动居中
    "initialCols": 120,
    "initialRows": 30,
    // "launchMode": "focus",
    "keybindings": [
        {
            "id": "Terminal.CopyToClipboard",
            "keys": "ctrl+c"
        },
        {
            "id": "Terminal.PasteFromClipboard",
            "keys": "ctrl+v"
        },
        {
            "id": "Terminal.DuplicatePaneAuto",
            "keys": "alt+shift+d"
        }
    ],
    "newTabMenu": [
        {
            "type": "remainingProfiles"
        }
    ],
    "profiles": {
        "defaults": {
            "colorScheme": "Tokyo Night Storm",
            "cursorShape": "bar",
            "font": {
                "face": "JetBrainsMono Nerd Font",
                "size": 11,
                "weight": "extra-black"
            },
            "historySize": 9001,
            "opacity": 75,
            "padding": "15",
            "scrollbarState": "hidden",
            "useAcrylic": true
        },
        "list": [
            {
                "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                "hidden": false,
                "name": "PowerShell"
            },
            {
                "commandline": "cmd.exe",
                "guid": "{574e775e-4f2a-5b96-ac1e-a2962a402336}",
                "hidden": false,
                "name": "Command Prompt"
            },
            {
                "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
                "hidden": false,
                "name": "Azure Cloud Shell",
                "source": "Windows.Terminal.Azure"
            },
            {
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "Command Prompt"
            }
        ]
    },
    "schemes": [
        {
            "background": "#24283B",
            "black": "#1D202F",
            "blue": "#7AA2F7",
            "brightBlack": "#414868",
            "brightBlue": "#7AA2F7",
            "brightCyan": "#7DCFFF",
            "brightGreen": "#9ECE6A",
            "brightPurple": "#BB9AF7",
            "brightRed": "#F7768E",
            "brightWhite": "#C0CAF5",
            "brightYellow": "#E0AF68",
            "cursorColor": "#C0CAF5",
            "cyan": "#7DCFFF",
            "foreground": "#C0CAF5",
            "green": "#9ECE6A",
            "name": "Tokyo Night Storm",
            "purple": "#BB9AF7",
            "red": "#F7768E",
            "selectionBackground": "#364A82",
            "white": "#A9B1D6",
            "yellow": "#E0AF68"
        }
    ],
    "showTabsInTitlebar": true,
    "tabWidthMode": "compact",
    "theme": "dark",
    "themes": [],
    "windowingBehavior": "useNew"
}
```

# 四、使用nvim

1. 安装

```powershell
winget install Neovim.Neovim
```

2.配置文件目录

```powershell
mkdir "$env:LOCALAPPDATA\nvim"
```

3.安装lazynvim插件，lua脚本如下

```lua
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.notify("Installing lazy.nvim...", vim.log.levels.INFO)
  -- 使用字符串命令，在 Windows 下更可靠
  local cmd = string.format(
    'git clone --filter=blob:none --branch=stable "https://github.com/folke/lazy.nvim.git" "%s"',
    lazypath
  )
  vim.fn.system(cmd)
  
  -- 检查是否真的安装成功
  if not vim.loop.fs_stat(lazypath) then
    error("Failed to install lazy.nvim. Please check your Git installation and network.")
  end
end
vim.opt.rtp:prepend(lazypath)

require("lazy").setup({
  spec = {
    { "LazyVim/LazyVim", import = "lazyvim.plugins" },
    { "folke/tokyonight.nvim", lazy = false, priority = 1000 },
    { "nvim-lualine/lualine.nvim", dependencies = { "nvim-tree/nvim-web-devicons" } },
  },
  defaults = { lazy = true, version = false },
  install = { colorscheme = { "tokyonight" } },
  checker = { enabled = true, notify = false },
  performance = {
    rtp = {
      disabled_plugins = {
        "gzip", "matchit", "matchparen", "netrwPlugin", "tarPlugin", "tohtml", "tutor", "zipPlugin",
      },
    },
  },
})
```