#### 1.GitHub上新建仓库
#### 2.gitbash here(桌面或者项目要放置的磁盘内) ，命令行输入```git clone git@github.com:Haluluyo/QQ-music.git```将项目文件夹下载至本地
![复制.png](https://upload-images.jianshu.io/upload_images/6426975-4c7c53108f2d2cf2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 3.cd到项目文件夹内
#### 4.命令行输入```git init``` //把这个目录变成Git可以管理的仓库
#### 5.命令行输入```ssh-keygen -t rsa -C "lulijuan_00@163.com"```，接着出现：
```
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):
```
请直接按下回车，然后系统会自动在.ssh文件夹（C:\Users\lenovo\.ssh）下生成两个文件，id_rsa和id_rsa.pub，用记事本打开id_rsa.pub，将全部的内容复制

![创建公钥1.png](https://upload-images.jianshu.io/upload_images/6426975-29f732ffed0612a9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![复制id_rsa.pub.png](https://upload-images.jianshu.io/upload_images/6426975-9703187a194bf4e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

打开https://github.com/，登陆账户，进入设置，进入ssh设置，点击New SSH key
![创建公钥2.png](https://upload-images.jianshu.io/upload_images/6426975-addda047fa4bd43b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在key中将刚刚复制的粘贴进去，点击Add SSH key
![创建公钥3.png](https://upload-images.jianshu.io/upload_images/6426975-1021a35b64142886.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 6.命令行输入：
 ```ssh -T git@github.com```//验证是否成功
```git config --global user.name "Haluluyo"```
```git config --global user.email "lulijuan_00@163.com"```
```git remote add origin git@github.com:Haluluyo/QQ-music``` //关联远程仓库
![](https://upload-images.jianshu.io/upload_images/6426975-002827468db6585f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 7.敲代码，保存，命令行输入：
```git add .```
```git commit -am "addfile"```
#####注：在push命令前一定要```git add .```
![](https://upload-images.jianshu.io/upload_images/6426975-a5a9fbc2adf9a8bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```git push origin master```
![](https://upload-images.jianshu.io/upload_images/6426975-a75c2f1a7e5f8a78.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


