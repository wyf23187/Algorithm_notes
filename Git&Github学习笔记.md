<div align='center' ><font size='30'>Git/Github学习笔记</font></div>

<center>Wyf</center>

[TOC]

# 1.Git中文件的状态

## 1.1 commited

当一个文件的所有修改都被保存在本地的 repo 中时，该文件就处于**提交的（committed）** 状态。处于提交阶段的文件是可以被推送到远程 repository(**repo**)（在 GitHub 上）的文件。

## 1.2 modified

处于**修改（modified）** 状态的文件已经做了一些修改，但还没有保存。这意味着该文件的状态与之前在提交状态下的状态有了改变。

## 1.3 staged

处于**暂存（staged）** 状态的文件意味着它可以被提交了。在这种状态下，所有必要的修改都已经完成，所以下一步就是把文件移到提交状态。

# 2.如何用Git进行文件处理

## 2.1 在 Git 中添加文件

当我们第一次初始化我们的项目时，该文件没有被 Git 追踪到。要做到这一点，我们使用这个命令`git add .`，将添加当前目录下所有文件。如果你想添加一个特定的文件，也许是一个名为`about.txt`的文件，你可以用`git add about.txt`。

现在，文件已经处于暂存状态（**staged state**）。这条命令之后你不会得到回应，但要知道你的文件处于什么状态，你可以运行`git status`命令。

## 2.2 在 Git 中提交文件

文件下一个状态处于提交状态（**committed state**）。为了提交我们的文件，我们使用`git commit -m "first commit"`命令。

命令的第一部分 "git commit "告诉 Git，所有被暂存的文件都准备好提交了，所以是时候进行快照了。第二部分 `-m "first commit"` 是提交信息。`-m`是信息的缩写，而括号内的文字是提交信息。从而进入（**committed state**）。

# 3.推送repository到Github

## 3.1 创建一个repo

登录Github账号，创建一个新的repository。具体步骤略。

## 3.2 从本地推送

eg: ==command==

```
git remote add origin https://github.com/ihechikara/git-and-github-tutorial.git
git branch -M main
git push -u origin main
```

**第一个命令** `git remote add origin [https://github.com/ihechikara/git-and-github-tutorial.git](https://github.com/ihechikara/git-and-github-tutorial.git)`，在你的本地 repo 和 Github 上的远程 repo 之间建立连接。

远程项目的 URL 应该与上面的完全不同。所以要根据你的实际 URL，确保你是按照步骤，用你自己的远程 repo 工作。执行这个命令后，你通常不会得到回应，但要确保你有互联网连接。

**第二个命令** `git branch -M main` 将主分支的名字改为 "main"。默认的分支可能被创建为 "master"，但 "main "是现在这个 repo 的标准名称。这里通常没有回应。

**第三个命令** `git push -u origin main` 将你的 repo 从本地设备推送到 GitHub。

# 4. Git的branch

## 4.1 branch的好处

有了分支(**branch**)，你可以在==不破坏原始副本的情况下，创建一个你想要处理的文件副本==。你可以把这些修改合并到原始副本上，或者让分支保持独立。

我想在列表中添加更多的任务，但我还不确定是否要把它们放在主列表中。因此，我将创建一个名为 `test` 的新分支，看看加入更多任务后我的列表会是什么样子。

## 4.2 创建新的branch

要创建一个新的分支，运行这个命令。`git checkout -b test`。

`checkout`告诉 Git 它应该切换到一个新的分支。`-b`告诉 Git 创建一个新的分支。`test`是要创建和切换到的分支的名字。

我们从上次提交的状态中创建了新的分支。现在让我们为这个新分支添加更多任务。要把新的状态合并到主分支（**main branch**）。必须先把这个分支分阶段并提交，详见`3.推送repository到Github`

## 4.3 Merge branch

提交完测试分支后，通过运行以下命令切换回主分支，`git checkout main`。

==注意==：我们没有添加`-b`，这是因为我们不是在创建一个新的分支，而是切换到一个现有的分支。你可以通过运行`git branch`命令来检查你的 repo 中存在的所有分支。

现在，我们可以通过运行`git merge test`，将测试分支中的修改合并到主分支中。这时，你会看到测试分支中的所有改动都反映在主分支中。

==ps==：如果你继续将你的 repo 推送到 GitHub，你会发现测试分支不会被推送。它只会保留在你的本地 repo 中。如果你想推送你的测试分支，可以用`git checkout test`切换到该分支，然后运行`git push -u origin test`。

# 5.通过Git在Github上拉取repo

## 5.1 拉取repo的好处

在 Git 中拉取意味着将远程仓库的当前状态克隆到你的电脑/仓库中。当你想在不同的电脑上操作你的仓库时，或者当你在网上为一个开源项目做贡献时，这就很方便了。

## 5.2 步骤

==Step1.== 进入 GitHub，在你的仓库的主页上，你应该看到一个绿色的按钮，上面写着 "code"。当你点击这个按钮时，你应该在一个下拉菜单中看到一些选项。继续并复制 HTTPS URL。

==Step2.== 导航到你想要将存储库克隆到的目标文件夹。在终端中输入以下命令：`git clone <repository-url> <folder-name>`，其中 `<repository-url>` 是你要克隆的 GitHub 存储库的 URL，`<folder-name>` 是你要将存储库克隆到的文件夹的名称。

例如，如果你要将名为 `my-repository` 的 GitHub 存储库克隆到名为 `my-folder` 的文件夹中，你可以在终端中输入以下命令：

```
git clone https://github.com/your-username/my-repository.git my-folder
```







