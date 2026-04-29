# Git 入门练习记录

## 1. Git 在解决什么问题

Git 记录项目每一次有意义的变化。你可以：

- 知道自己改了哪些文件。
- 把一组修改保存成一次提交。
- 回看历史。
- 开分支做实验，不影响主线。
- 和 GitHub 上的远程仓库同步。

## 2. 三个本地状态

```text
工作区 working tree -> 暂存区 staging area -> 提交 commit
```

常用命令：

```bash
git status
git diff
git add notes.md
git commit -m "Update notes"
```

含义：

- `git status`：看当前仓库状态。
- `git diff`：看工作区还没暂存的具体修改。
- `git add`：选择哪些修改进入下一次提交。
- `git commit`：创建一个历史快照。

## 3. 分支开发

刚才实际练过的流程：

```bash
git switch -c feature/add-run-count
git add app.js notes.md
git commit -m "Add run count demo"
git switch main
git merge feature/add-run-count
```

含义：

- `git switch -c xxx`：创建并切换到新分支。
- 在功能分支上开发，不直接污染 `main`。
- `git merge xxx`：把功能分支合并回当前分支。

## 4. 远程同步

本练习里用了一个本地裸仓库模拟 GitHub：

```bash
git remote add practice-origin ../git-learning-remote.git
git push -u practice-origin main
git pull --ff-only
```

真实 GitHub 仓库通常用 `origin` 这个名字：

```bash
git remote add origin https://github.com/YOUR_NAME/git-learning-sandbox.git
git branch -M main
git push -u origin main
```

之后日常使用：

```bash
git pull --rebase origin main
git push
```

## 5. 学源码项目时的安全习惯

在大项目里先做这几件事：

```bash
git status --short --branch
git remote -v
git log --oneline --graph --decorate --all --max-count=10
```

提交前一定先看：

```bash
git diff
git diff --cached
```

不要把 `.env`、密钥、token、模型权重、临时日志提交到 GitHub。

