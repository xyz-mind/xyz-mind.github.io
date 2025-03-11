---
title: Git与GitHub操作全流程详解
description: >-
  Git与GitHub操作全流程详解
author: 刘十五
date: 2025-03-11 22:56:00 +0800
categories: [Blogging, Tutorial]
tags: [Python笔记]
pin: true
media_subpath: '/posts/20250311'
---

以下是 Git 与 GitHub 从仓库创建到项目推送与拉取的全流程详细操作指南：

---

### **一、环境准备**
#### 1. 安装 Git
- **Windows**：访问 [Git 官网](https://git-scm.com/) 下载安装包，默认选项安装。
- **macOS**：使用 Homebrew 安装：`brew install git`
- **Linux**：通过包管理器安装（如 Ubuntu/Debian：`sudo apt install git`）。

#### 2. 配置 Git
设置全局用户名和邮箱（提交代码时显示作者信息）：
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

### **二、本地仓库创建与操作**
#### 1. 初始化本地仓库
```bash
# 进入项目目录
cd your-project-folder

# 初始化 Git 仓库
git init
```
- 这会创建一个隐藏的 `.git` 文件夹，记录版本信息。

#### 2. 添加文件到暂存区
```bash
# 添加所有修改的文件
git add .

# 添加单个文件
git add filename.txt
```

#### 3. 提交到本地仓库
```bash
git commit -m "提交说明（如：初始化项目）"
```
- `-m` 参数后填写本次提交的描述信息（需简洁明确）。

---

### **三、GitHub 远程仓库操作**
#### 1. 创建 GitHub 远程仓库
1. 登录 [GitHub](https://github.com)。
2. 点击右上角 **+** → **New repository**。
3. 输入仓库名称（如 `my-project`），选择公开（Public）或私有（Private），点击 **Create repository**。

#### 2. 关联本地仓库与远程仓库
复制 GitHub 仓库的 HTTPS 或 SSH 地址（推荐 SSH）：
```bash
# 添加远程仓库地址（命名为 origin）
git remote add origin git@github.com:your-username/your-repo.git

# 查看已关联的远程仓库
git remote -v
```

---

### **四、推送代码到 GitHub**
#### 1. 首次推送（本地 → 远程）
```bash
git push -u origin main
```
- `-u` 参数将本地 `main` 分支与远程 `main` 分支关联，后续推送可直接用 `git push`。
- 若本地分支名为 `master`，需改为 `git push -u origin master`（GitHub 默认分支已从 `master` 改为 `main`）。

#### 2. 后续推送
```bash
git add .
git commit -m "更新说明"
git push
```

---

### **五、从 GitHub 拉取代码**
#### 1. 克隆仓库（首次获取代码）
```bash
git clone git@github.com:your-username/your-repo.git
```

#### 2. 拉取远程最新代码（本地已关联仓库）
```bash
# 拉取远程 main 分支的更新
git pull origin main
```

---

### **六、分支管理**
#### 1. 创建与切换分支
```bash
# 创建并切换到新分支 dev
git checkout -b dev

# 查看所有分支
git branch
```

#### 2. 合并分支
```bash
# 切换回 main 分支
git checkout main

# 将 dev 分支合并到 main 分支
git merge dev
```

#### 3. 推送分支到远程
```bash
# 推送本地 dev 分支到远程（远程不存在时会自动创建）
git push origin dev
```

---

### **七、协作流程（Pull Request）**
1. **Fork 仓库**：在 GitHub 上将他人仓库 Fork 到自己的账号。
2. **克隆到本地**：`git clone git@github.com:your-username/forked-repo.git`
3. **创建特性分支**：`git checkout -b feature-branch`
4. **修改并提交代码**：
   ```bash
   git add .
   git commit -m "添加新功能"
   git push origin feature-branch
   ```
5. **发起 Pull Request**：在 GitHub 仓库页面点击 **Compare & pull request** 提交 PR，等待审核合并。

---

### **八、常见问题**
#### 1. 权限被拒绝（Permission Denied）
- **原因**：未配置 SSH 密钥。
- **解决**：
  1. 生成 SSH 密钥：`ssh-keygen -t ed25519 -C "your.email@example.com"`
  2. 将公钥 `~/.ssh/id_ed25519.pub` 内容添加到 GitHub **Settings → SSH and GPG keys**。

#### 2. 忽略文件（如 node_modules）
创建 `.gitignore` 文件，写入需忽略的文件名或目录：
```
node_modules/
*.log
.env
```

#### 3. 冲突解决
拉取代码时若出现冲突：
1. 手动编辑冲突文件（冲突标记为 `<<<<<<<` 和 `>>>>>>>`）。
2. 解决冲突后提交：
   ```bash
   git add .
   git commit -m "解决冲突"
   git push
   ```

---

通过以上流程，你可以完成 Git 与 GitHub 的仓库管理、代码推送与拉取操作。建议多练习分支操作和协作流程以熟悉团队开发模式。