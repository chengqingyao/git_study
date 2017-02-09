2017年2月9日15:26:15

git基本使用方式：
1.创建版本库
    在要创建版本库的目录下面运行 git init 命令，git就会自动在当前目录下面创建一个 .git 的文件夹，用于保存相关的信息
 
2.在版本库中添加一个文件
    使用 git add readme.txt 命令来将文件添加到版本库中
    
3.向版本库中提交修改
    使用命令 git commit -m "此次提交的相关说明"
    
4.查看版本库的当前状态
    使用命令 git status

git版本回退：
1.查看版本提交日志
    使用命令 git log，可以看到每个版本的相关信息，其中我们需要的就是 commit 号
    注：这样直接使用还显示出了其它的一些信息，可以使用如下的命令来精简输出
        git log --pretty=oneline
    
2.回退到上一版本
    会退到上一个版本使用命令：git reset --hard HEAD^
    注意：上一个版本使用 HEAD^ 表示，上上个版本使用 HEAD^^ 表示，上100个版本可以简写为 HEAD~100
          git内部使用一个指针 HEAD 指向当前版本，当切换版本的时候实际上就是移动这个 HEAD 指针，指向不同的版本
          
3.切换到指定版本
    使用命令： git reset --hard 版本号，注意：版本号不需要写全，写几位即可，git会自动去查找
    
4.查看提交记录以及回退记录
    使用命令：git reflog
    
git修改管理方式
1.git在版本库中存在一个缓冲区，以及一个版本分支，使用 git add 命令的时候会自动将添加文件的修改加入到缓冲区中
  一旦使用命令：git commit，就会将缓冲区中的修改一块添加到版本分支中
2.使用git时，在每次修改文件后，需要先将修改加入到缓冲区中，然后再提交到版本分支中    
    
git撤销修改的方式
1.文件修改的内容还没有提交到暂存区时，可以使用 git checkout -- filename, 来将文件恢复到当前版本的初始状态
2.文件修改的内容已经提交到暂存区时，可以使用 git reset HEAD readme.txt  , 来删除暂存区中的修改
3.文件修改的内容已经提交到版本库时，可以选择回退到上一版本
    
git文件删除方式
1.需要使用命令：git rm 文件名，删除指定文件
2.如果删除错误，只要这个文件提交到版本库中，那么可以使用 git checkout -- 文件名，将误删文件恢复到最新状态，前提是不能使用 git rm删除版本库中的文件


远程仓库
1.生成ssh key
    使用命令 ssh-keygen -t rsa -C "youremail@example.com"，如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

2.在github上面添加
    settings -> SSH and GPG keys 中
       title任意填
       key文本框中粘贴：id_rsa.pub 的内容，github通过这个公钥来判断提交修改的人
       
3.在Github创建一个远程仓库
    Create a new repo

4.将本地版本库和远程版本库关联起来
    git remote add origin git@github.com:xxxx/xxxx
    远程库的名字就是origin
    
5.将本地库的内容推送到远程库上
    git push -u origin master
    实际上就是讲当前的master分支推送到远程库，第一推送时，加上 -u 选项，不但可以推送，还会讲本地库和远程库关联起来
    
6.提交修改到到远程库
    git push origin master
    
7.ssh警告
    第一次使用push命令时，会出一个警告，直接 yes 就可以
    
    
克隆远程库
1.首先在github上面创建一个测试的远程库
2.git clone https://github.com/chengqingyao/git_clone_test.git 
