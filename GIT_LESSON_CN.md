# Git 互动练习课：从修改文件到 push

## 0. 背景

我们现在在一个专门用来学习 Git 的练习仓库里：

```text
/home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-sandbox
```

外层目录：

```text
/home/ps/dcr/claudecode/claudecode_sourcecode1
```

本身也是一个 Git 仓库。为了避免把学习内容误提交到源码项目里，本课所有命令都必须在
`git-learning-sandbox` 目录里执行。

这次我们采用互动方式：

1. 我先写清楚当前要做什么。
2. 你在终端执行命令。
3. 你把终端输出发给我。
4. 我根据真实输出继续更新这份 lesson。

## 1. 本课使用哪些文件

本课主要使用这几个文件：

```text
README.md
GIT_LESSON_CN.md
notes.md
app.js
.gitignore
```

其中最重要的是：

```text
notes.md
```

我们会把 `notes.md` 当作练习修改的文件。原因是它很简单，不涉及程序运行，适合用来观察
Git 的状态变化。

这份文件：

```text
GIT_LESSON_CN.md
```

是课程记录文件。你每完成一步并把终端输出发给我，我会继续把真实过程整理到这里。

## 2. 本课想学习哪些 Git 操作

本课只学习从“修改文件”到“推送远程”的基础流程：

```text
查看状态 -> 修改文件 -> 查看差异 -> 暂存 -> 提交 -> 推送
```

对应命令是：

```bash
pwd
git status --short --branch
git diff notes.md
git add notes.md
git status
git diff --cached
git commit -m "Practice Git add commit push flow"
git status --short --branch
git push
git status --short --branch
```

暂时不学习：

```text
branch
merge
rebase
conflict
pull request
reset
stash
```

这些后面再单独学。

## 3. 每个阶段文件会是什么样子

### 阶段 A：开始前

`notes.md` 已经在仓库里，并且有一些旧内容。此时我们还没有进行本轮新修改。

Git 状态大概会是：

```text
## main...practice-origin/main
 M GIT_LESSON_CN.md
 M README.md
```

这里的 `M GIT_LESSON_CN.md` 是因为我正在重写这份 lesson。

### 阶段 B：修改 notes.md 后

你会在 `notes.md` 最后加一行，例如：

```markdown
- Third practice: I will record every Git command output.
```

此时文件内容发生变化，但还没有进入暂存区。

Git 状态里会出现：

```text
 M notes.md
```

注意左边有一个空格，右边有 `M`：

```text
 M
```

这表示文件在工作区被修改了，但还没有 `git add`。

### 阶段 C：执行 git add 后

运行：

```bash
git add notes.md
```

此时 `notes.md` 的修改进入暂存区。

Git 状态会变成类似：

```text
M  notes.md
```

注意这次是左边有 `M`，右边是空格：

```text
M 
```

这表示文件已经暂存，准备进入下一次 commit。

### 阶段 D：执行 git commit 后

运行：

```bash
git commit -m "Practice Git add commit push flow"
```

此时 `notes.md` 的修改会变成一次本地提交。

如果本地提交还没有推送到远程，状态会出现：

```text
## main...practice-origin/main [ahead 1]
```

`ahead 1` 的意思是：本地比远程多 1 个提交。

### 阶段 E：执行 git push 后

运行：

```bash
git push
```

本地提交会被推送到远程。

推送成功后，`ahead 1` 应该消失：

```text
## main...practice-origin/main
```

这表示本地和远程同步。

## 4. 本轮命令和终端记录

请严格按这个顺序执行。每执行一组，就把终端输出发给我。

### 第 1 组：确认你在正确目录

要执行的命令：

```bash
pwd
git status --short --branch
```

你的真实终端输出：

```text
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ pwd
git status --short --branch
/home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-sandbox
## main...practice-origin/main
 M GIT_LESSON_CN.md
 M README.md
```

解释：

- 当前目录正确：

```text
/home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-sandbox
```

- `git status --short --branch` 的意思：

```text
git status
```

查看当前 Git 仓库状态。

```text
--short
```

使用短格式输出。短格式更适合学习文件状态，因为它会用两列字符表示文件在不同区域的状态。

例如：

```text
 M README.md
M  notes.md
```

第一列表示暂存区，第二列表示工作区。

```text
 M README.md
```

表示 `README.md` 在工作区被修改了，但还没有进入暂存区。

```text
M  notes.md
```

表示 `notes.md` 已经进入暂存区，准备提交。

```text
--branch
```

把当前分支和远程跟踪关系也显示出来。

- 当前分支是 `main`，并且它正在跟踪 `practice-origin/main`：

```text
## main...practice-origin/main
```

这一行可以拆开理解：

```text
##
```

表示这是分支信息行，不是文件状态行。

```text
main
```

表示你当前所在的本地分支叫 `main`。

```text
practice-origin/main
```

表示当前本地分支正在跟踪的远程分支。这里的 `practice-origin` 是远程仓库名字，
`main` 是远程仓库里的分支名字。

```text
main...practice-origin/main
```

表示 Git 正在比较本地 `main` 和远程 `practice-origin/main` 的关系。

如果后面没有 `[ahead 1]` 或 `[behind 1]`，说明本地和远程在提交历史上是同步的。

- 现在有两个文件被修改：

```text
 M GIT_LESSON_CN.md
 M README.md
```

其中 `GIT_LESSON_CN.md` 是我正在编辑的 lesson，`README.md` 是之前重写过的说明文档。
本轮我们先不处理它们，先专注练习 `notes.md`。

### 第 2 组：修改 notes.md 并查看状态

现在请打开 `notes.md`，在最后增加这一行：

```markdown
- Third practice: I will record every Git command output.
```

保存后执行：

```bash
git status --short
git diff notes.md
```

你的真实终端输出：

```diff
diff --git a/notes.md b/notes.md
index e213028..8d2a713 100644
--- a/notes.md
+++ b/notes.md
@@ -8,3 +8,4 @@
 - Simulated a teammate pushing a remote change.
 
 ### 我现在做了一个小小改动
+- Third practice: I will record every Git command output.
\ No newline at end of file
```

解释：

```text
diff --git a/notes.md b/notes.md
```

表示 Git 正在比较 `notes.md` 的旧版本和新版本。

```text
--- a/notes.md
+++ b/notes.md
```

`a/notes.md` 可以理解为修改前的文件，`b/notes.md` 可以理解为修改后的文件。

```text
@@ -8,3 +8,4 @@
```

这是位置提示，说明这次差异发生在文件第 8 行附近。旧版本这里有 3 行，新版本这里有 4 行。

```diff
+- Third practice: I will record every Git command output.
```

前面的 `+` 是 diff 标记，表示这一行是新增的。真正写进文件的内容是：

```markdown
- Third practice: I will record every Git command output.
```

```text
\ No newline at end of file
```

表示文件最后没有换行符。这不是严重错误，但通常文本文件建议最后保留一个换行。

下一步我们会先把 `notes.md` 放进暂存区。

### 第 3 组：暂存 notes.md

要执行的命令：

```bash
git add notes.md
git status --short
git diff --cached notes.md
```

你的真实终端输出：

```text
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git add notes.md
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git status --short
 M GIT_LESSON_CN.md
 M README.md
M  notes.md
```

```diff
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git diff --cached notes.md
diff --git a/notes.md b/notes.md
index e213028..8d2a713 100644
--- a/notes.md
+++ b/notes.md
@@ -8,3 +8,4 @@
 - Simulated a teammate pushing a remote change.
 
 ### 我现在做了一个小小改动
+- Third practice: I will record every Git command output.
\ No newline at end of file
```

解释：

```bash
git add notes.md
```

这条命令没有输出是正常的。在 Unix/Linux 命令里，很多命令成功时默认保持安静。

`git add notes.md` 的作用是：把 `notes.md` 当前的修改放进暂存区。

```text
M  notes.md
```

这个状态来自刚才这条命令：

```bash
git status --short
```

`git status` 是查看仓库状态；`--short` 表示用短格式显示。

短格式状态的每一行通常长这样：

```text
XY 文件名
```

这里的 `X` 和 `Y` 不是字母本身，而是两个位置占位符：

- `X` 位置：暂存区状态，也就是这个文件有没有被 `git add`。
- `Y` 位置：工作区状态，也就是这个文件在 `git add` 之后还有没有新的修改。

可以把它理解成：

```text
第 1 列 第 2 列 文件名
暂存区 工作区 文件名
```

常见例子：

```text
 M file.txt
```

第 1 列是空格，第 2 列是 `M`，表示：文件在工作区被修改了，但还没有暂存。

```text
M  file.txt
```

第 1 列是 `M`，第 2 列是空格，表示：文件已经暂存，暂存后没有继续修改。

```text
MM file.txt
```

第 1 列和第 2 列都是 `M`，表示：文件有一部分修改已经暂存，但暂存后又继续改了这个文件。

所以：

```text
M  notes.md
```

表示：

- 第一列是 `M`：`notes.md` 的修改已经在暂存区。
- 第二列是空格：`notes.md` 在 `git add` 之后没有新的未暂存修改。

对比：

```text
 M README.md
```

表示：

- 第一列是空格：`README.md` 没有进入暂存区。
- 第二列是 `M`：`README.md` 在工作区被修改了。

```bash
git diff --cached notes.md
```

这里的 `--cached` 表示“看暂存区里的差异”。也就是说，这个命令显示的是：

```text
如果我现在 commit，notes.md 会提交哪些内容？
```

你看到新增的这一行：

```diff
+- Third practice: I will record every Git command output.
```

说明 `notes.md` 的目标修改已经准备好进入下一次提交。

### 第 4 组：提交 notes.md

要执行的命令：

```bash
git commit -m "Practice Git add commit push flow"
git status --short --branch
git log --oneline --graph --decorate --all --max-count=8
```

你的真实终端输出：

```text
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git commit -m "Practice Git add commit push flow"
[main 45de9eb] Practice Git add commit push flow
 1 file changed, 1 insertion(+)
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git status --short --branch
## main...practice-origin/main [ahead 1]
 M GIT_LESSON_CN.md
 M README.md
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git log --oneline --graph --decorate --all --max-count=8
* 45de9eb (HEAD -> main) Practice Git add commit push flow
* 06dd1d9 (practice-origin/main) Add my first Git learning note
* 7e92626 Add Chinese Git lesson notes
* 3f263df Simulate teammate note update
* 340bfac (feature/add-run-count) Add run count demo
* 3eddcd6 Initial git learning project
```

解释：

```text
[main 45de9eb] Practice Git add commit push flow
```

这表示 Git 创建了一次新提交：

- `main`：提交发生在本地 `main` 分支。
- `45de9eb`：这次提交的短哈希，可以理解为这次快照的编号。
- `Practice Git add commit push flow`：提交信息。

```text
1 file changed, 1 insertion(+)
```

表示这次提交包含 1 个文件变化，新增了 1 行。

```text
## main...practice-origin/main [ahead 1]
```

表示本地 `main` 比远程 `practice-origin/main` 多 1 个提交。

这个状态正好说明：你已经完成了本地提交，但还没有推送到远程。

```text
 M GIT_LESSON_CN.md
 M README.md
```

这两个文件仍然只是工作区修改，没有进入刚才的 commit。刚才的 commit 只提交了
`notes.md`，因为之前只执行了：

```bash
git add notes.md
```

```text
* 45de9eb (HEAD -> main) Practice Git add commit push flow
* 06dd1d9 (practice-origin/main) Add my first Git learning note
```

这两行说明：

- `HEAD -> main` 在 `45de9eb`：你的本地 `main` 最新提交是 `45de9eb`。
- `practice-origin/main` 在 `06dd1d9`：远程 `main` 还停在旧提交。
- 所以本地领先远程 1 个提交，对应状态里的 `[ahead 1]`。

### 终端提示符解释

你看到的这一段：

```text
(vllm-env) ➜  git-learning-sandbox git:(main) ✗
```

不是 Git 命令输出，而是你的 shell 提示符。它在每次等待你输入命令时出现。

可以拆成几部分：

```text
(vllm-env)
```

表示当前激活的 Python/Conda 环境叫 `vllm-env`。这和 Git 没有直接关系，
只是说明当前终端正在使用这个环境里的 Python、pip 等工具。

```text
➜
```

这是 shell 主题显示的提示符箭头，表示“现在可以输入命令了”。它没有特殊 Git 含义。

```text
git-learning-sandbox
```

表示当前所在目录的名字。完整路径是：

```text
/home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-sandbox
```

```text
git:(main)
```

这是 shell 主题自动显示的 Git 信息，表示当前目录是一个 Git 仓库，并且当前分支是
`main`。

```text
✗
```

通常表示当前 Git 仓库不是干净状态，也就是还有未提交的修改。这里对应：

```text
 M GIT_LESSON_CN.md
 M README.md
```

所以这整行可以理解为：

```text
我在 vllm-env 环境里，当前目录是 git-learning-sandbox，这是一个 Git 仓库，
当前分支是 main，而且仓库里还有未提交修改。
```

### 第 5 组：接入真实 GitHub 远程

现在我们开始把本地练习仓库接到真实 GitHub 仓库。

你的 GitHub 仓库地址是：

```text
https://github.com/haichengmai20-hub/git-learning-sandbox
```

我已经把它加入本地 Git 配置，远程名字叫：

```text
origin
```

注意：`origin` 不是命令，它只是一个远程仓库名字。

你尝试运行了：

```text
origin https://github.com/haichengmai20-hub/git-learning-sandbox.git
```

终端输出：

```text
zsh: command not found: origin
```

解释：

这表示 shell 把 `origin` 当成一个命令去执行了，但系统里没有叫 `origin` 的命令。

正确理解是：

```text
origin = 远程仓库的名字
```

它要和 `git remote`、`git push`、`git fetch` 这些 Git 命令一起使用，例如：

```bash
git remote -v
git push origin main
git fetch origin
```

你随后运行了正确的检查命令：

```bash
git remote -v
```

你的真实终端输出：

```text
(vllm-env) ➜  git-learning-sandbox git:(main) ✗ git remote -v

origin  https://github.com/haichengmai20-hub/git-learning-sandbox.git (fetch)
origin  https://github.com/haichengmai20-hub/git-learning-sandbox.git (push)
practice-origin /home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-remote.git (fetch)
practice-origin /home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-remote.git (push)
```

解释：

现在这个本地仓库有两个远程：

```text
origin
```

真实 GitHub 远程仓库。

```text
practice-origin
```

本机上的模拟远程仓库。

`fetch` 表示从这个远程下载信息；`push` 表示向这个远程上传提交。

### 本地仓库和远程仓库的区别

本地仓库是你电脑上的这个目录：

```text
/home/ps/dcr/claudecode/claudecode_sourcecode1/git-learning-sandbox
```

它包含：

- 你正在编辑的文件。
- 本地 `.git` 历史。
- 本地分支，比如 `main`。
- 还没有上传的本地提交。

远程仓库是另一个位置上的 Git 仓库。本课里现在有两个远程：

```text
practice-origin = 本机模拟远程
origin = GitHub 真实远程
```

可以这样理解：

```text
本地仓库 local repository
  |
  | git push
  v
远程仓库 remote repository
```

反过来：

```text
远程仓库 remote repository
  |
  | git fetch / git pull
  v
本地仓库 local repository
```

`git commit` 只影响本地仓库。

`git push` 才会把本地提交上传到远程仓库。

`git fetch` 会把远程信息下载到本地，但不会自动改你的工作文件。

`git pull` 会下载远程信息，并尝试合并到当前分支。

### 为什么不直接推到 GitHub main

你的 GitHub 网页显示，这个仓库已经有一次提交：

```text
Initial commit
```

并且 GitHub 上已经有：

```text
.gitignore
LICENSE
README.md
```

而我们本地练习仓库也已经有自己的提交历史：

```text
3eddcd6 -> ... -> 45de9eb
```

这两边不是同一条历史线。直接推送到 GitHub 的 `main` 可能会被拒绝，或者需要处理
README 等文件冲突。

为了让学习过程更顺滑，我们先不碰 GitHub 的 `main`，而是推送到 GitHub 的一个新分支：

```text
practice/local-git-learning
```

这样可以安全地在 GitHub 网页上看到本地练习内容，又不会破坏 GitHub 的 `main`。

### 第 6 组：把本地练习内容推到 GitHub 新分支

要执行的命令是：

```bash
git push -u origin main:practice/local-git-learning
git status --short --branch
git log --oneline --graph --decorate --all --max-count=8
```

这个命令的含义：

```text
git push
```

上传提交。

```text
origin
```

上传到真实 GitHub 远程。

```text
main:practice/local-git-learning
```

把本地 `main` 分支推送成 GitHub 上的新分支 `practice/local-git-learning`。

```text
-u
```

设置上游跟踪关系。以后这个分支继续 push 时可以少写远程和分支名。

执行完把终端输出发给我。我会继续记录，并解释 GitHub 网页上应该去哪里看这个新分支。
