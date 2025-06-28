# git

## git 基本命令
```bash
git clone <ssh网址># 克隆远程仓库(ssh在github上有)
##修改文件后
git checkout <your_branch_name> #切换到你的分支
git add .
git commit -m "修改了什么"
git push 
```


```bash
#更新
git pull
```

解决冲突
1.两个分支修改后都要保存到本地
```bash
git add .
git commit -m "-------"
```
2.切换分支后，进行合并，并提交

