# 什么是 Git 和 GitHub？

**Git**是一个分布式版本控制系统，用于跟踪和管理软件代码的变更。它可以帮助团队协同开发，记录代码的历史变更，并允许开发者在不同分支上进行并行开发。

**GitHub**则是一个基于 Git 的代码托管平台。它提供了一个在线的仓库托管服务，使开发者能够在云端存储代码、进行协作、管理问题跟踪和代码审阅。

# 安装 Git

首先，你需要在本地计算机上安装 Git。你可以从 [官方网站](https://git-scm.com/) 下载适合你操作系统的安装程序。

# Git 基础

## 初始化仓库

1. 在你的项目文件夹中打开命令行或终端。
2. 使用以下命令初始化一个新的 Git 仓库：

```bash
git init
```

## 添加和提交更改

1. 编辑或添加你的文件。
2. 使用以下命令将更改添加到暂存区：

```bash
git add 文件名
```

3. 使用以下命令提交暂存区的更改到版本历史：

```bash
git commit -m "提交说明"
```

## 查看状态和历史

- 查看工作区和暂存区状态：

```bash
git status
```

- 查看提交历史：

```bash
git log
```

## 创建分支

- 创建新分支：

```bash
git branch 新分支名
```

- 切换到分支：

```bash
git checkout 分支名
```

## 合并分支

- 切换回主分支（或接受分支）：

```bash
git checkout 主分支名
```

- 合并分支到主分支：

```bash
git merge 要合并的分支名
```

## 远程仓库连接

1. 在 GitHub 上创建一个新仓库。
2. 关联本地仓库和远程仓库：

```bash
git remote add origin 远程仓库URL
```

3. 将本地分支推送到远程仓库：

```bash
git push -u origin 主分支名
```

## 克隆远程仓库

使用以下命令克隆远程仓库到本地：

```bash
git clone 远程仓库URL
```

## 发起 Pull Request

1. 在 GitHub 上切换到要提交的分支。
2. 点击“Pull Request”按钮。
3. 填写请求的详细信息和描述，然后点击“Create Pull Request”。

## 处理 Issues

1. 在仓库页面点击“Issues”选项卡。
2. 点击“New Issue”创建一个新的问题。
3. 填写问题描述，添加标签等，然后点击“Submit New Issue”。

## 进行 Code Review

1. 在 Pull Request 页面，查看提交的更改。
2. 添加评论、建议修改或批准更改。