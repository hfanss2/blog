---
title: github 图床使用免费CDN加速-jsdelivr
date: 2025-06-25 17:52:22
tags: 
- github图床
- 免费CDN图床
categories: 
- 免费图床
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/124.jpg
newimg: true
comments: true
zhailu: 使用github+jsdelivr制作的免费CDN图床，右键一键上传，复制粘贴使用，快捷方便，居家旅行必备 (◕‿◕)。
---

github做图床大部分人都知道，但是国内访问速度不稳定，所以使用jsdelivr加速。

jsdelivr是什么呢？它是一个免费、快速和可信赖的CDN加速服务，直接集成在github中的，无需额外操作即可使用。

本文分两部份，最终实现的效果是：

在本地文件夹中某图片上点击鼠标右键，选中 上传至github图床，稍等片刻，在需要使用的地方直接Ctrl+v粘贴即可。

## 一、怎么使用jsdelivr

## 二、通过脚本一键上传图片至github，并返回地址到粘贴板

先来说第一部分

```
1.在github上创建一个项目，githubpic,公开项目
2.随便上传一张图片xx.jpg
3.访问CDN地址，第一个老是失联，目前用第二个
https://cdn.jsdelivr.net/gh/github用户名/仓库名@master/xx.jpg
https://gcore.jsdelivr.net/gh/github用户名/仓库名@master/xx.jpg

这里注意一下，@master是jsdelivr默认的版本，不跟github的走，即github现在默认创建的原始分支是main(早前是master),访问CDN的时候还是@master
```

这一部分结束，基本上就算作使用了CDN了，但我们日常操作肯定不会这么麻烦的去传，所以这里我结合这篇文章 [个人图床的最简单制作-腾讯云COS](https://blog.csdn.net/q2158798/article/details/82354216) 做了个简单的脚本实现一键上传，一键使用

第二部分，一键上传

### 1.github申请ssh密钥

这一部分网上很多，大家可自行搜索，也可看我找的这篇[文章](https://blog.csdn.net/crasowas/article/details/137211646)，最终实现的就是拉取、上传代码都是免密的效果

### 2.将刚才的项目githubpic拉取到某个目录(建议D盘)下，使用ssh拉取

### 3.处理脚本

#### 3.1在C盘根目录下创建目录commitGithub，在目录中创建commit.bat，打开编辑，将下列内容粘贴进去保存，注意修改其中的基础目录为仓库本地目录

```bat
@echo off
chcp 65001 >nul  :: 设置 cmd 为 UTF-8 编码
:: =============================================
:: 功能：右键上传图片到 Git (SSH方式) 并返回网络地址
:: 使用方法：右键图片 → 选择"上传到Git"（需先配置SSH密钥）
:: =============================================
::1.设置基础目录-必设,你的仓库拉取下来的本地路径
set "base=D:\githubpic"
set "image_file=%~1"

:: 2. 进入文件所在目录（确保 Git 命令在正确目录执行）
cd /d "%~dp1"

:: 3. 检查是否是 Git 仓库
git rev-parse --is-inside-work-tree >nul 2>&1
if errorlevel 1 (
    echo 错误：当前目录不是 Git 仓库！
    pause
    exit /b
)

:: 4. 添加文件到暂存区并提交
git add "%image_file%"
set "commit_message=上传文件: %~nx1"
git commit -m "%commit_message%"

:: 5. 使用SSH方式推送（不再转换地址，直接推送）:: 如果是其他分支，修改为对应分支名
git push origin main || (
    echo ❌ Git 推送失败，错误代码: %ERRORLEVEL%
    pause
    exit /b %ERRORLEVEL%
)

echo ✅ Git 推送成功，继续执行后续操作...

:: --------提交成功，下面开始拼装CDN路径--------
:: 6. 获取 Git 远程SSH地址（用于生成网络访问URL）
for /f "tokens=*" %%A in ('git config --get remote.origin.url') do set "git_remote=%%A"

:: 检查是否是SSH地址（如 git@github.com:user/repo.git）
echo %git_remote% | findstr "git@" >nul
if errorlevel 1 (
    echo 错误：当前远程地址不是SSH格式！请使用SSH地址（如 git@github.com:user/repo.git）
    pause
    exit /b
)

::  如果有二级目录，这里会拆分路径
set "dir=%~dp1"
call set "p=%%dir:%base%=%%"
set "p=%p:\=/%"
if not "%p:~0,1%"=="/" set "p=/%p%"
if not "%p:~-1%"=="/" set "p=%p%/"


set "image_name=%~nx1"
set "image_file_path=%p%%image_name%"

:: 7. 生成网络访问URL（GitHub示例）将SSH地址转换为HTTPS格式的raw地址
:: 替换SSH地址为HTTPS-jsdelivr-CDN地址（GitHub）
set "git_remote_https=%git_remote:git@github.com:=%"
:: jsdelivr的CDN地址经常被污染，特提供几个替代地址，以便不时之需，如果全部被污染，那就没办法了，替换下面的前缀即可
:: https://gcore.jsdelivr.net/gh/  短暂测试，这个地址的失联率最低，暂时用这个
:: https://testingcf.jsdelivr.net/gh/
:: https://cdn.jsdelivr.net/gh/    这个地址经常跳转到 raw.github的网站上，相当于没有启用CDN
set "git_remote_https=https://gcore.jsdelivr.net/gh/%git_remote_https:.git=%"
:: 下面这个是开启jsdelivr的CDN加速的地址,目前github最新建的项目是main版本，但是jsdelivr还是默认master版本
set "image_network_url=%git_remote_https%@master%image_file_path%"
:: 8. 输出网络地址
echo 图片已上传！网络访问地址：
echo %image_network_url%

:: 复制到剪贴板（需 clip 命令支持）
echo %image_network_url% | clip
echo 地址已复制到剪贴板！

echo 已上传完毕，Ctrl + v 即可粘贴，窗口将在5秒后关闭...
timeout /t 5 /nobreak >nul
exit
```

#### 3.2添加右键快捷键

```
WIN+R调用运行库，输入regedit，会打开注册表编辑器
找到目录 计算机\HKEY_CLASSES_ROOT\*\shell
```

在shell上右键新建项：上传github图床，在 上传github图床  上右键新建项：command,如图：

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/001.png)



右侧双击默认，修改值为：

```
cmd.exe /K "C:\commitGithub\commit.bat "%1""
```

至此，大功告成。

使用的话，把图片拖到本地项目目录下，右键点击  上传github图床  等待命令执行完即可

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/002.png)

成功状态：

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/003.png)

上传成功的图片大概会有1分钟-5分钟延时。