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

## 处理冲突

在 Git 中，冲突通常发生在多个开发者同时修改同一文件的相同部分时。解决冲突的过程包括以下步骤：

1. 当多个人修改了同一文件的相同部分并提交到仓库或者操作不当的时候，在进行 `git merge` 之后，Git 会标记出冲突的地方。你可以通过以下命令查看文件的冲突：

```bash
git status
```

2. 手动解决冲突：打开包含冲突的文件，你会看到类似以下的标记：

```plaintext
<<<<<<< HEAD
// Your changes
=======
// Changes from others
>>>>>>> other_branch
```

你需要手动选择要保留的更改，删除标记符号，并将文件修改为你期望的最终状态。

3. 标记为已解决：解决冲突后，使用 `git add` 标记文件为已解决：

```bash
git add filename
```

4. 提交更改：提交你的解决方案：

```bash
git commit -m "Resolve conflict in filename"
```

5. 继续合并或推送：如果你是在合并分支，完成所有冲突解决后，可以继续合并：

```bash
git merge other_branch
```

如果你是在推送更改，使用以下命令：

```bash
git push origin branch_name
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

# Git 多人协作

一般来说我们使用 Github 或者 Gitee 等远程托管平台通过 Git 进行项目的多人协作，这其中主要包含两种，一种是团队内部的协作，一种是外界的开源式的协作，以下以 Github 为例。

## 添加 Collaborators

在 Github 中添加 Collaborators，等于说在你的项目中成为了类似于管理员的身份，你具有直接对项目进行修改的权限，这种操作的方式对于小型的项目来说是一种具有性价比的操作，但是对于大型项目来说，collaborators 的存在无疑为这个项目添加了一些权限过高的成员，这样对于项目的统筹管理其实并不恰当。

## Fork 项目

一种在多人协作中更加恰当的操作流程是对于项目进行 fork。对于 fork，一种简单的理解可以理解为是你在 GitHub 上针对这个项目复制出来了一个分支，并且这个分支归你所有。

具体从表象上来看，你的仓库中会多出一个该项目的仓库，这个仓库中的内容与该项目当时时刻的内容完全相同，但是并不会在后续实时更新，相反的，你需要在 Github 中的界面进行手动的更新，这一步的操作与本地的 Merge 极为类似。

![[Git sync fork.png]]

在这里选择 Sync fork 就可以更新仓库。

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

## Github workflow

在了解了诸多的基础知识的之后，接下来是参加开源项目的完整工作流介绍。

![[Git workflow.png]]

首先，在 GitHub 上 Fork 一个项目，并且在本地配置了 Git Config 之后，在命令行串口中使用 `git clone` 指令将仓库克隆到本地，这个被直接克隆的分支被称为 `main branch`。

其次，在本地建立一个分支，称之为 `dev branch`，这个分支存在的必要在于，使自己修改的内容与 GitHub 上的内容之间存在 `main branch` 作为隔离。通过 `git merge` 将 `main branch` 内容复制到 `dev branch`。

此时可以开始进行你自己的工作，在每一次工作前使用 `git pull` 更新你的 `main branch`，并且将 `main branch` 再次进行 `git merge` 到 `dev branch`，理论来说应当不存在冲突，如存在冲突，处理冲突。

将分支切换到 `dev branch`，并且开始你的工作，更改完毕之后使用 `git add` 以及 `git commit` 记录更改，并切换到 `main branch` 分支，将 `dev branch` 进行 `git merge` 到 `main branch`。

最后，使用 `git push` 将 `main branch` 上传到远程仓库，并且在 GitHub 页面的仓库中发起 Pull Request。