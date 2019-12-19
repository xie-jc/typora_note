①下载->安装时选择use from git bash only(其余的全next)   ②安装好后配置环境变量(到bin目录)   ③可以有多个版本库,版本库又称为分支,默认分支为master

#### 1、配置ssh免密登录

①打开gitbash   ②配置用户:git config --global user.{name/email} "name/email"   ③配置本地秘钥:ssh-keygen -t rsa -C 之前配置的email   ④登录github.com->settings->ssh and ...->new->将本地.ssh目录下的公钥复制填写   ⑤测试连通性:ssh -T git@github.com

#### 2、关联远程分支

①新建本地版本库(文件夹)->git init   ②在远程库创建版本库，一般在github上创建:profile->new(得到ssh或者http标识)   ③关联:git remote add origin ssh/http标识

#### 3、常用命令

​    (1)第一次发布 

​    ①git add .   ②git commit -m “描述”   ③git push -u origin master

​    (2)第一次下载

​    ①git clone 资源标识   

​    (3)提交/更新

​    ①提交:git pull   ②更新:和发布比仅为第三步命令无“ -u ”

4、原理图

|           git架构原理           |           svn架构原理           |
| :-----------------------------: | :-----------------------------: |
| ![](D:\jim\typora\tool\git.png) | ![](D:\jim\typora\tool\svn.png) |





