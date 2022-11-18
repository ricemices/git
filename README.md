## 建立本地仓库

``` bash
git init //把这个目录变成Git可以管理的仓库
git add README.md //文件添加到仓库
git add . //不但可以跟单一文件，还可以跟通配符，更可以跟目录。一个点就把当前目录下所有未追踪的文件全部add了 
git commit -m "first commit" //把文件提交到仓库
git remote add origin git@github.com:wangjiax9/practice.git //关联远程仓库
git push -u origin master //把本地库的所有内容推送到远程库上 git push -u origin master -f
```

## 关联仓库

``` bash
git remote add origin giturl.git
```

## 解除关联

``` bash
git remote rm origin
```

## 生成ssh-key

``` bash
ssh-keygen -t rsa -C "email@163.com"
```

## 配置git

``` bash
git config --global user.name "name"
git config --global user.email "Email@163.com"

git config --global --unset http.https://github.com.proxy
```

## 状态查询

``` bash
git status
```

## 分支查询

``` bash 
git branch -a
```

## 切换分支

``` bash 
git checkout 分支名
```










## 其它


由于当前本地的代码也是从其他的git仓库上clone下来的，所以就不需要执行sudo git init命令了。
1.sudo git add . ----将当前目录下的所有文件添加到版本库。
2.sudo git commit -m “一些说明” ----把添加的文件提交到仓库
3.sudo git remote add origin 新的远程git仓库的地址 ----关联到新的远程库的地址

由于我们当前的代码是从其他的git仓库上clone下来的，所以当前的关联仍然是之前的git地址，所以这一步会失败，并出现如下的错误信息：
fatal: remote origin already exists.
此时我们需要将之前的关联的git地址删除，然后再关联新的git仓库地址。具体操作如下：
sudo git remote rm origin
再执行第三步：sudo git remote add origin 新的远程git仓库的地址。—origin是远程仓库的别名
关联成功后就可以使用sudo git remote -v 命令查看是否关联到了新的git仓库地址。
4.sudo git push -u origin 需要push到新的远程仓库的分支名。----由于我们本地可能有好几个分支，可以使用git branch -v 命令查看。选择自己需要push到新的git仓库的分支名origin。
如下面所示，是将aaaa分支push到上面关联的远程库中。
git push -u origin aaaa
5.sudo git status ----状态查询
发现一个我问题：在从新的仓库上clone下来的代码，会出现如下警告：
warning: remote HEAD refers to nonexistent ref, unable to checkout.
并且进入工程目录，发现没有任何文件。通过git branch -a命令查看分支情况，发现没有master分支，只有我们上面上传的aaaa分支remotes/origin/aaaa。所以此时需要使用命令：sudo git checkout aaaa切换到aaaa的分支，这时就有之前我们上传push上的代码了。
主要原因是我们直接sudo git clone 下来的代码默认是master分支，由于我们新的git仓库上面没有master分支，所以clone下来的时候就是空的，因为master分支就是空的嘛，这是切换到自己之前提交的那个分支上就可以了。
如果想在新的仓库上clone下来的代码是master分支，可以采取如下的方法：
首先删除原有的git信息：sudo rm -r .git
然后执行如下步骤：

``` bash
sudo git init
sudo git add .
sudo git commit -m “说明”---------执行完这一步后，使用git branch -v就可以看到master分支了。
sudo git remote add origin 新的仓库路径
sudo git push -u origin master
```
参考文档：

https://www.cnblogs.com/yaoxc/p/3946280.html
https://blog.csdn.net/njnujuly/article/details/86011600
