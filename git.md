# git

## git工作流程

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git1.png)

1. 工作区：修改文件的地区，不进入版本历史；
2. 暂存区：暂时保存未提交的代码，不进入版本历史；关键指令为git add
3. 本地仓库：附带提交信息并保存，进入版本历史；关键指令为给git commit
4. 远程仓库：把本地仓库上传给远程仓库，他人可查看，用于备份代码（github）；关键指令：git push；

- git pull（拉取）：查看远程仓库别的代码并复制；
- git fetch：查看远程更新内容；
- git merge：确认更新正确合并到自己代码；

## git 命令



### 克隆仓库

git clone +远程仓库网址（eg ：https://github.com/username/repo.git） 

cd + 文件名（eg  ：cd repo）进入克隆仓库的文件

### 创建新分支

git checkout -b + 文件名

### 暂存文件

git add + 文件名（保存该文件到暂存区）

git add . （保存所有修改的文件到暂存区）

### 提交更改

git commit -m + “提交信息”

### 拉取最新更改

git pull + 远程仓库名(origin) + 要合并的远程仓库的分支名(main)；

git pull + 远程仓库名(origin) + 新的分支文件名（在新的分支上工作）

### 推送更改

git push + 远程仓库名(origin) + 提交的文件名（将本地的提交推送到远程仓库）

### 创建pull request

在 GitHub 或其他托管平台上创建 Pull Request，邀请团队成员进行代码审查。PR 合并后，你的更改就会合并到主分支

### 合并更改

在 PR 审核通过并合并后，可以将远程仓库的主分支合并到本地分支：

```
git checkout main（主分支）
git pull origin main
git merge new-feature
```

### 删除分支

如果不再需要新功能分支，可以将其删除：

```
git branch -d new-feature
```

或者从远程仓库删除分支：

```
git push origin --delete new-feature
```

##  工作区 暂存区 版本库

- **工作区：**就是你在电脑里能看到的目录。

- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。

- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

	![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git2.png)

	-  图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存（stage/index），标记为 "master" 的是 master 分支所代表的目录树。
	-  图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。
	-  图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。
	-  当对工作区修改（或新增）的文件执行 **git add** 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。
	-  当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。
	-  当执行 **git reset HEAD** 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
	-  当执行 **git rm --cached <file>** 命令时，会直接从暂存区删除文件，工作区则不做出改变。
	-  当执行 **git checkout .** 或者 **git checkout -- <file>** 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区中的改动。
	-  当执行 **git checkout HEAD .** 或者 **git checkout HEAD <file>** 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。
	
	###  1.工作区
	
	工作区为本地计算机的项目目录，可删除 修改 创建文件，并且包含了当前项目的所有文件和子目录，可显示项目的当前状态。
	
	### 2.暂存区
	
	临时存储文件的区域，包含了即将提交到版本库的文件快照，保存了将被包括在下一个提交中的更改，也可使用 git add 多次提交文件到暂存区。
	
	```
	git add filename       # 将单个文件添加到暂存区
	git add .              # 将工作区中的所有修改添加到暂存区
	git status             # 查看哪些文件在暂存区中
	```
	
	### 3.版本库
	
	版本库包含所有项目的历史记录；
	
	**特点：**
	
	- 版本库分为本地版本库和远程版本库。这里主要指本地版本库。
	
	- 本地版本库存储在 `.git` 目录中，它包含了所有提交的对象和引用。
	
		**常用命令：**
	
		```
		git commit -m "Commit message"   # 将暂存区的更改提交到本地版本库
		git log                          # 查看提交历史
		git diff                         # 查看工作区和暂存区之间的差异
		git diff --cached                # 查看暂存区和最后一次提交之间的差异
		```

## 工作区、暂存区和版本库之间的关系

### **1、工作区 -> 暂存区**

**使用 git add 命令将工作区中的修改添加到暂存区。**

```
git add filename
```

### 2、暂存区 -> 版本库

使用 git commit 命令将暂存区中的修改提交到版本库。

```
git commit -m "Commit message"
```

### 3、版本库 -> 远程仓库

使用 git push 命令将本地版本库的提交推送到远程仓库。

```
git push origin branch-name
```

### 4、远程仓库 -> 本地版本库

使用 git pull 或 git fetch 命令从远程仓库获取更新。

```
git pull origin branch-name
# 或者
git fetch origin branch-name
git merge origin/branch-name
```

## git创建仓库


### git init

使用该命令初始化一个git版本库，之后git仓库会生成一个.git文件。使用时进入想要创建的目标仓库目录或新建仓库目录

```
mkdir my-project（创建新的仓库目录）
cd my-project（打开该仓库目录）
git init （当前目录下输入就可以创建版本库）
```

如果当前目录下有几个文件要加进版本库，先用git add 添加 之后 git commit 提交

### git config

配置仓库

## git 基本操作

### 创建仓库命令

#### git init

初始化仓库

#### git clone

使用git clone可以复制当前现有git仓库的项目

```
git clone <仓库地址>
git clone <仓库地址><新名字>（克隆了git仓库的项目目录并命名为新名字）
```

repo 为git仓库，dire为本地目录

```
eg : git clone https://github.com/tianqixin/runoob-git-test
```

git命令使用后会自动将远程仓库的所有分支和历史记录复制到本地

### 提交与修改

#### git add

```
git add [file1] [file2] ...（将一个或多个文件添加到暂存区）
git add . （将当前目录下的所有文件添加到暂存区）
git add -all （暂存整个仓库所有已跟踪和未跟踪文件的变更，不包含上一级仓库）
```

#### git status

查看当前git仓库当前状态，可以查看上次提交之后是否有对文件进行更改

git status 命令会显示以下信息：

- 当前分支的名称。
- 当前分支与远程分支的关系（例如，是否是最新的）。
- 未暂存的修改：显示已修改但尚未使用 `git add` 添加到暂存区的文件列表。
- 未跟踪的文件：显示尚未纳入版本控制的新文件列表。

1. 使用 **-s** 参数来获得简短的输出结果：

```
$ git status -s
AM README
A  hello.php
```

2.使用 -b 显示当前分支信息

3.--ignored ： 显示被忽略的文件

4.--untracked-files=<mode> ： 控制未跟踪文件的显示方式

```
git status -s -- git/typora笔记（指定路径）
```

**第一列**字符表示**版本库**与**暂存区**之间的比较状态。
**第二列**字符表示**暂存区**与**工作区**之间的比较状态。

​       表示文件未发生更改

`M` 表示文件发生改动。
`A` 表示新增文件。
`D` 表示删除文件。
`R` 表示重命名。
`C` 表示复制。
`U` 表示更新但未合并。
`?` 表示未跟踪文件。
`!` 表示忽略文件。

#### git diff

git diff 命令显示已写入暂存区和已经被修改但尚未写入暂存区文件的区别，即比较文件在暂存区与工作区的差异

- 尚未缓存的改动：**git diff**
- 查看已缓存的改动： **git diff --cached****（或git diff – staged)（最后一次提交到版本库中的文件和暂存区中文件的修改对比）
- 查看已缓存的与未缓存的所有改动：**git diff HEAD**（已经提交到版本库中的文件和未提交到版本库中的文件的所有修改对比）
- 显示摘要而非整个 diff：**git diff --stat**

#### git difftool

用外部工具查看和比较文件更改

#### git range - diff

用于比较两个提交范围之间的差异。

```
git range-diff <old-range> <new-range>
```

- **`<old-range>`**：旧的提交范围或分支。
- **`<new-range>`**：新的提交范围或分支。

#### git commit

将暂存区内容添加到本地仓库中

```
git commit -m [message]
git commit [file1] [file2] ... -m [message]（提交暂存区指定文件到仓库区）
git commit -a（设置-a参数后不用git add 直接提交）
```

####  git reset

用于回退版本，可以指定退回某一次提交的版本

```
git reset [--soft | --mixed | --hard] [HEAD]
```

**--mixed** 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

**--soft** 参数用于回退到某个版本：

```
eg ： git reset --soft HEAD~3   # 回退上上上一个版本 
```

**--hard** 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：

- HEAD 表示当前版本

- HEAD^ 上一个版本

- HEAD^^ 上上一个版本

- HEAD^^^ 上上上一个版本

	

- HEAD~0 表示当前版本

- HEAD~1 上一个版本

	

	HEAD^2 上上一个版本

- HEAD^3 上上上一个版本

**git reset HEAD** 命令用于取消已缓存的内容。执行该命令用于取消该文件因git add 添加到暂存区，也就是暂存区没有该文件修改的新版本

#### git rm

git rm 用于删除文件

1. 将文件从暂存区和工作区中删除：

```
git rm <file>
```

2.强行从暂存区和工作区中删除修改后的文件：

```
git rm -f <file>
```

3.把文件从暂存区移除，但仍在工作目录中（仅在跟踪清单中删除）

```
git rm --cached <file>
```

#### git mv

git mv 命令用于移动或重命名一个文件、目录或软连接。

```
git mv [file] [newfile]
```

如果新文件名已经存在，但还是要重命名它，可以使用 **-f** 参数：

```
git mv -f [file] [newfile]
```

#### git notes

允许用户将附加注释添加到提交中

```
git notes <subcommand> [options] [arguments]
```

- **`<subcommand>`**：具体的操作子命令（如 `add`, `show`, `list`, `remove`, `edit`, `merge` 等）。
- **`[options]`**：命令的选项或参数。
- **`[arguments]`**：命令的附加参数，如提交哈希值等。

#####  1.git notes add

**将新的注释添加到提交中。**

- **`-m`**：指定注释的内容。

- **`<commit-hash>`**：指定要添加注释的提交（可选，默认为当前提交）。

	```
	# 添加注释到当前提交
	git notes add -m "This commit fixes the login bug"
	
	# 添加注释到特定提交
	git notes add -m "Added new feature X" <commit-hash>
	```

#####  2.git notes show

**显示提交的注释。**

- **`<commit-hash>`**：指定要显示注释的提交（可选，默认为当前提交）。

##### 3.git notes list

**列出当前分支上所有提交的注释。**

##### 4.git notes remove

**删除提交的注释。**

```
git notes remove <commit-hash>
```

##### **5.git notes edit**

**编辑提交的注释。与 `git notes add` 类似，但在编辑模式下打开默认编辑器进行注释编辑。**

##### **`6.git notes merge`**

**合并不同的注释记录**。

##### **`7.refs/notes/*`**

**用于指定注释的引用路径**。用于推送和拉取注释。

```
# 推送注释到远程仓库
git push origin refs/notes/*
```

#### git check out

用于在不同的分支之间切换、恢复文件、创建新分支等操作。

```
git checkout <branch-name>（从当前分支切换到指定分支）
git checkout -b <new-branch-name>（创建新分支并切换）
git checkout -（切换到前一个分支）
git checkout -- <file>（将指定文件恢复到最近一次提交时的状态，丢弃未提交的更改）
git checkout <commit-hash>（切换到指定提交）
git checkout tags/<tag-name>（如果你有一个标签 <tag-name>，你可以使用这个命令来切换到该标签所指向的提交状态。）
```

#### git switch

作用与 [git checkout](https://www.runoob.com/git/git-checkout.html) 类似，但提供了更清晰的语义和错误检查。

```
git switch <branch-name>（从当前分支切换到指定的分支 <branch-name>）
git switch -c <new-branch-name>（创建新分支并切换到该分支）
git switch -（切换到前一个分支）
git switch <commit_hash>（恢复工作目录到某个特定的提交状态）
git switch -d（使切换到某个提交的操作更明确，即使存在同名分支也不会切换到分支上。）
git switch -f（强制执行切换，即使有更改未提交）
git branch（列出可用的本地分支和标签，便于选择切换目标）
```

#### git restore

用于恢复或撤销文件的更改，可以恢复工作区和暂存区中的文件，也可以用于丢弃未提交的更改。

```
git restore [<options>] [<pathspec>...]
```

- **`<pathspec>`**：要恢复的文件或目录路径。
- **`<options>`**：用于定制恢复行为的选项。

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git3.png)

#### git show

用于查看提交、标签、树对象或其他 Git 对象的内容。这个命令对于审查提交历史、查看提交的具体内容以及调试 Git 对象非常有用。

```
git show [<options>] [<object>]
```

- **`<object>`**：指定要显示的 Git 对象。可以是提交哈希、标签、分支名等。
- **`<options>`**：显示的选项或格式设置。

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git4.png)

常用：

1. **显示提交的详细信息**

```
git show <commit-hash>
```

**2、显示提交的差异**

**3、显示提交的文件列表**（显示提交中更改的文件名）

**4、显示提交的统计信息**

**5、使用自定义格式显示提交信息**

**6、显示标签的详细信息**

```
git show <tag>
```

### 提交日志

#### git log

**git log** 显示了从最新提交到最早提交的所有提交信息，包括提交的哈希值、作者、提交日期和提交消息等。

```
git log [选项] [分支名/提交哈希]
```

- `-p`：显示提交的补丁（具体更改内容）。
- `--oneline`：以简洁的一行格式显示提交信息。
- `--graph`：以图形化方式显示分支和合并历史。
- `--decorate`：显示分支和标签指向的提交。
- `--author=<作者>`：只显示特定作者的提交。
- `--since=<时间>`：只显示指定时间之后的提交。
- `--until=<时间>`：只显示指定时间之前的提交。
- `--grep=<模式>`：只显示包含指定模式的提交消息。
- `--no-merges`：不显示合并提交。
- `--stat`：显示简略统计信息，包括修改的文件和行数。
- `--abbrev-commit`：使用短提交哈希值。
- `--pretty=<格式>`：使用自定义的提交信息显示格式。

#####  常用选项

限制显示的提交数:

```
git log -n <number>
```

显示自指定日期之后的提交：

```
git log --since="2024-01-01"
```

显示指定日期之前的提交：

```
git log --until="2024-07-01"
```

只显示某个作者的提交：

```
git log --author="Author Name"
```

#### git blame

可以追踪文件中每一行的变更历史，包括作者、提交哈希、提交日期和提交消息等信息。

```
git blame [选项] <文件路径>
```

- `-L <起始行号>,<结束行号>`：只显示指定行号范围内的代码注释。
- `-C`：对于重命名或拷贝的代码行，也进行代码行溯源。
- `-M`：对于移动的代码行，也进行代码行溯源。
- `-C -C` 或 `-M -M`：对于较多改动的代码行，进行更进一步的溯源。
- `--show-stats`：显示包含每个作者的行数统计信息。

#### git shortlog

用于总结 Git 仓库的提交历史，提供对每位作者的提交计数以及每个提交类别的概览。

```
git shortlog [<options>] [<revision-range>]
```

- **`<revision-range>`**：指定要生成摘要的提交范围，默认为当前分支的全部提交。

- **`<options>`**：用于定制输出格式或行为的选项。

	![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git5.png)

#### git describe

用于生成版本号，帮助识别特定的提交，并能够在构建、发布或追踪特定版本时使用。

```
git describe [<options>] [<commit>]
```

- **`<commit>`**：指定要描述的提交。默认为当前提交。
- **`<options>`**：用于定制输出格式或行为的选项。

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git6.png)

### 远程操作

####  git remote

用于管理git仓库中的远程仓库

- `git remote`：列出当前仓库中已配置的远程仓库。
- `git remote -v`：列出当前仓库中已配置的远程仓库，并显示它们的 URL。
- `git remote add <remote_name> <remote_url>`：添加一个新的远程仓库。指定一个远程仓库的名称和 URL，将其添加到当前仓库中。
- `git remote rename <old_name> <new_name>`：将已配置的远程仓库重命名。
- `git remote remove <remote_name>`：从当前仓库中删除指定的远程仓库。
- `git remote set-url <remote_name> <new_url>`：修改指定远程仓库的 URL。
- `git remote show <remote_name>`：显示指定远程仓库的详细信息，包括 URL 和跟踪分支。

#### git fetch

用于从远程获取代码库，执行git fetch 后 执行git merge 合并

```
git fetch origin
git merge origin/master
```

#### git pull

用于从远程获取代码并合并本地的版本,为git fetch 和git merge 合并

```
git pull [远程仓库名] [分支名]
```

- `[远程仓库名]` 通常是 `origin`，是默认的远程仓库名。
- `[分支名]` 是你要合并的远程分支，比如 `main` 或 `master`。

#### git push

用于从将本地的分支版本上传到远程并合并。

命令格式如下：

```
git push <远程主机名> <本地分支名>:<远程分支名>
```

如果本地分支名与远程分支名相同，则可以省略冒号：

```
git push <远程主机名> <本地分支名>
```

如果本地版本与远程版本有差异，但又要强制推送可以使用 --force 参数：

```
git push --force origin master
```

删除主机的分支可以使用 --delete 参数，以下命令表示删除 origin 主机的 master 分支：

```
git push origin --delete master
```

#### git submodule

用于管理包含其他 Git 仓库的项目,对于大型项目或需要将外部库集成到项目中的情况非常有用。 通过使用子模块，你可以将外部库作为你的项目的一部分来管理，而不必将其直接合并到主仓库中。

**使用详解**

**1、初始化子模块**

```
git submodule init
```

该命令会初始化配置文件中的所有子模块。它会根据 .gitmodules 文件中的信息设置子模块的 URL 和路径，但不会下载子模块的内容。

**常见用法：**在克隆了一个包含子模块的仓库后，运行此命令来初始化子模块。

```
git clone <repo-url>
cd <repo-dir>
git submodule init
```

**2、更新子模块**

```
git submodule update
```

该命令会从子模块的远程仓库中拉取子模块的内容，并将其更新到 .gitmodules 文件中指定的提交。

**常见用法：**在初始化子模块后，或当你需要更新子模块的内容时，运行此命令。

```
git submodule update
```

**3、添加子模块**

```
git submodule add <repo-url> [<path>]
```

该命令会将指定的 Git 仓库作为子模块添加到当前仓库中。

`<repo-url>` 是子模块的仓库地址，`<path>` 是子模块在主仓库中的路径（可选，如果不指定，默认使用子模块仓库的名称作为路径）。

**常见用法：**将外部库作为子模块添加到项目中。

```
git submodule add https://github.com/example/libfoo.git libfoo
```

**4、移除子模块**

```
git submodule deinit [<path>]
git rm [<path>]
```

- `git submodule deinit <path>`：将子模块从 `.git/config` 文件中移除，并删除子模块目录中的文件。
- `git rm <path>`：将子模块的引用从主仓库中删除，并提交更改。

**常见用法：**从主仓库中移除一个子模块。

```
git submodule deinit libfoo
git rm libfoo
rm -rf .git/modules/libfoo
```

**5、列出子模块**

```
git submodule
```

列出当前仓库中的所有子模块，以及它们的提交哈希和路径。

**常见用法：**查看项目中所有子模块的状态。

```
git submodule
```

**6、更新所有子模块**

```
git submodule update --recursive --remote
```

- `--recursive`：递归地更新所有子模块（包括子模块的子模块）。
- `--remote`：从子模块的远程仓库拉取最新的更改。

**常见用法：**当子模块包含其他子模块时，确保所有层级的子模块都更新到最新版本。

```
git submodule update --recursive --remote
```

**7、检查子模块状态**

```
git submodule status
```

显示子模块的当前状态，包括当前的提交哈希和路径，是否有未提交的更改。

**常见用法：**查看子模块的当前状态。

```
git submodule status
```

### git 文件状态

**文件状态分为三种**：工作目录（Working Directory）、暂存区（Staging Area）、本地仓库（Local Repository）。

#### 工作目录

为在计算机上可以看到的项目文件，是实际操作文件的地方，包括查看，编辑，删除和创建文件，对文件的更改都在工作目录中

工作目录中的文件两种状态

- **未跟踪（Untracked）**：新创建的文件，未被 Git 记录。
- **已修改（Modified）**：已被 Git 跟踪的文件发生了更改，但这些更改还没有被提交到 Git 记录中。

#### 暂存区

保存提交到本地仓库中的更改

```
git add <filename>  # 添加指定文件到暂存区
git add .           # 添加所有更改到暂存区
```

#### 本地仓库

本地仓库是一个隐藏在 `.git` 目录中的数据库，用于存储项目的所有提交历史记录。每次你提交更改时，Git 会将暂存区中的内容保存到本地仓库中。

使用 `git commit -m "commit message"` 命令将暂存区中的更改提交到本地仓库。

```
git commit -m "commit message"  # 提交暂存区的更改到本地仓库
```

### 文件状态的转换

#### **未跟踪（Untracked）**

 新创建的文件最初是未跟踪的。它们存在于工作目录中，但没有被 Git 跟踪。新建文件后没有任何操作就是未跟踪

#### **已跟踪（Tracked）**

通过 `git add` 命令将未跟踪的文件添加到暂存区后，文件变为已跟踪状态。

#### **已修改（Modified）**

 对已跟踪的文件进行更改后，这些更改会显示为已修改状态，但这些更改还未添加到暂存区。

```
echo "Hello, World!" > newfile.txt  # 修改文件
git status                          # 查看状态，显示 newfile.txt 已修改
```

#### **已暂存（Staged）**

使用 `git add` 命令将修改过的文件添加到暂存区后，文件进入已暂存状态，等待提交。

#### **已提交（Committed）**

使用 `git commit` 命令将暂存区的更改提交到本地仓库后，这些更改被记录下来，文件状态返回为已跟踪状态。

## git 分支管理

使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作，一条分支代表一条独立的开发线

### 创建分支

#### 创建新分支并切换到该分支：

```
git checkout -b <branchname>
```

#### 切换分支命令:

```
git checkout (branchname)
git switch
```

当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

### 查看分支

#### 查看所有分支：

```
git branch
```

#### 查看远程分支：

```
git branch -r
```

#### 查看所有本地和远程分支：

```
git branch -a
```

### 合并分支

将其他分支合并到当前分支：

```
git merge <branchname>
```

例如，切换到 main 分支并合并 feature-xyz 分支：

```
git checkout main
git merge feature-xyz
```

### 解决合并冲突

当合并过程中出现冲突时，Git 会标记冲突文件，你需要手动解决冲突。

打开冲突文件，按照标记解决冲突。

标记冲突解决完成：

```
git add <conflict-file>
```

提交合并结果：

```
git commit
```

### 删除分支

删除本地分支：

```
git branch -d <branchname>
```

强制删除未合并的分支：

```
git branch -D <branchname>
```

删除远程分支：

```
git push origin --delete <branchname>
```

如果我们要手动创建一个分支。执行 **git branch (branchname)** 即可，当你以此方式在上次提交更新之后创建了新分支，如果后来又有更新提交， 然后又切换到了 **testing** 分支，Git 将还原你的工作目录到你创建分支时候的样子。

### 命令手册

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git7.png)

##  git 恢复和回退

- **`git checkout`**：切换分支或恢复文件到指定提交。
- **`git reset`**：重置当前分支到指定提交（软重置、混合重置、硬重置）。
- **`git revert`**：创建一个新的提交以撤销指定提交，不改变提交历史。
- **`git reflog`**：查看历史操作记录，找回丢失的提交。

### 1、git checkout：检查出特定版本的文件

git checkout 命令用于切换分支或恢复工作目录中的文件到指定的提交。

恢复工作目录中的文件到某个提交：

```
git checkout <commit> -- <filename>
```

例如，将 file.txt 恢复到 abc123 提交时的版本：

```
git checkout abc123 -- file.txt
```

切换到特定提交：

```
git checkout <commit>
```

例如：

```
git checkout abc123
```

**切换到特定提交时处于分离头指针状态**

### 2、git reset：重置当前分支到特定提交

git reset 命令可以更改当前分支的提交历史，它有三种主要模式：--soft、--mixed 和 --hard。

**--soft**：只重置 HEAD 到指定的提交，暂存区和工作目录保持不变。

```
git reset --soft <commit>
```

**--mixed（默认）**：重置 HEAD 到指定的提交，暂存区重置，但工作目录保持不变。

```
git reset --mixed <commit>
```

**--hard**：重置 HEAD 到指定的提交，暂存区和工作目录都重置。

```
git reset --hard <commit>
```

例如，将当前分支重置到 abc123 提交：

```
git reset --hard abc123
```

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git8.png)

### 3、git revert：撤销某次提交

git revert 命令创建一个新的提交，用来撤销指定的提交，它不会改变提交历史，适用于已经推送到远程仓库的提交。

```
git revert <commit>
```

例如，撤销 abc123 提交：

```
git revert abc123
```

![](https://cdn.jsdelivr.net/gh/sakskadjas-a11y/note@master/image/image.git9.png)

### 4、git reflog：查看历史操作记录

git reflog 命令记录了所有 HEAD 的移动。即使提交被删除或重置，也可以通过 reflog 找回。

```
git reflog
```

利用 reflog 可以找到之前的提交哈希，从而恢复到特定状态。例如：

```
git reset --hard HEAD@{3}
```

## git 标签

如果你达到一个重要的阶段，并希望永远记住提交的快照，你可以使用 **git tag** 给它打上标签。Git 标签（Tag）用于给仓库中的特定提交点加上标记。比如说，我们想为我们的项目发布一个 "1.0" 版本，我们可以用 **git tag -a v1.0** 命令给最新一次提交打上（HEAD） "v1.0" 的标签。-a 选项意为"**创建一个带注解的标签**"，不用 -a选项也可以执行的，但它不会记录这标签是啥时候打的，谁打的，也不会让你添加个标签的注解，我们推荐一直创建带注解的标签。

### **标签语法格式：**

```
git tag <tagname>（使用该命令为轻量标签）
```

**-a** 选项可以添加注解：

```
$ git tag -a v1.0 （标签为附注标签）
```

### 推送标签到远程仓库

默认情况下，git push 不会推送标签，你需要显式地推送标签。

```
git push origin <tagname>
```

推送所有标签：

```
git push origin --tags
```

### 删除标签

轻量标签为只有哈希值，无其他信息

本地删除：

```
git tag -d <tagname>
```

远程删除：

```
git push origin --delete <tagname>
```

### 附注标签

附注标签存储了创建者的名字、电子邮件、日期，并且可以包含标签信息。附注标签更为正式，适用于需要额外元数据的场景。

创建附注标签语法：

```
git tag -a <tagname> -m "message"
```

PGP 签名标签命令：

```
git tag -s <tagname> -m "runoob.com标签"
```

查看标签信息：

```
git show <tagname>
```
