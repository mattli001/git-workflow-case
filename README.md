# git-workflow-case
modify of this.  
## 開出 feature/function-a 分支，進行功能開發
新增一個檔案，模擬 feature/function-a 的功能開發
```
git checkout -b feature/function-a origin/feature/function-a
touch function-a.txt
git add function-a.txt
git commit -m "[develop #1] add function a text."
```
此時 local 的 feature/function-a 有 cbb75c6 這個修改
```
* cbb75c6 (HEAD, feature/function-a) [develop #1] add function a text.
```

## 在 github 的 master，模擬 master 有新功能已開發
使用 github 的 edit 介面，修改 README.md  
當在 local 的 master，git pull 後，看到 master 有 aa3aeaf commit 
```
* aa3aeaf (HEAD, origin/master, origin/HEAD, master) Update README.md
```
## 切回 feature/function-a 同步 origin/master 的修改，並推回 github
推回 github 是想讓其它有共同開發 feature/function-a 的人，也能同步。
執行下面的操作
```
matt@matt-nb:/sdc1/Project/trunk/git-workflow-case/git-workflow-case$ git checkout feature/function-a 
Switched to branch 'feature/function-a'
Your branch is ahead of 'origin/feature/function-a' by 1 commit.
  (use "git push" to publish your local commits)
matt@matt-nb:/sdc1/Project/trunk/git-workflow-case/git-workflow-case$ git lol
* cbb75c6 (HEAD, feature/function-a) [develop #1] add function a text.
* 83ffd15 (origin/feature/function-a) 1. modify README.md
* 22163ea Initial commit
matt@matt-nb:/sdc1/Project/trunk/git-workflow-case/git-workflow-case$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: [develop #1] add function a text.
matt@matt-nb:/sdc1/Project/trunk/git-workflow-case/git-workflow-case$ git lol
* 16f96d4 (HEAD, feature/function-a) [develop #1] add function a text.
* aa3aeaf (origin/master, origin/HEAD, master) Update README.md
* 83ffd15 (origin/feature/function-a) 1. modify README.md
* 22163ea Initial commit
matt@matt-nb:/sdc1/Project/trunk/git-workflow-case/git-workflow-case$ git push
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 302 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:mattli001/git-workflow-case.git
   83ffd15..16f96d4  feature/function-a -> feature/function-a
```
