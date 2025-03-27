# git教程

## git安装Mac

1. 通过App Store安装Xcode, 会自动安装Git, 或使用Homebrew安装：`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. 打开终端, 输入以下命令：`git add .`
3. 输入以下命令：`git commit -m "COMMIT_MESSAGE"`
4. 输入以下命令：`git push origin master`

## git配置

1. 配置本地信息
    为了在后面上传项目到github时方便知道是谁上传的，需要给本机git配置用户名和邮箱：

    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "email@example.com"
    ```

    打开 git bash（也可任意位置右键打开 git bash），查看配置命令：`git config --list`

2. 配置SSH
    1. SSH与SSH Key是什么？
        要了解SSH key简介，首先得熟悉SSH，Secure Shell (SSH) 是一个允许两台电脑之间通过安全的连接进行数据交换的网络协议。SSH 密钥对可以让您方便的登录到 SSH 服务器，而无需输入密码。SSH 密钥对总是成双出现的，一把公钥，一把私钥。这里用到了非对称公钥加密体系，生成的公钥放到github的网站上，生成的私钥放在自己的电脑上。
    2. 生成SSH Key

        ```bash
        ssh-keygen -t rsa -C “注册邮箱”
        //执行后一直回车即可
        ```

    3. 获取ssh key公钥内容（id_rsa.pub）

        ```bash
        cd ~/.ssh
        cat id_rsa.pub
        ```

    4. 复制ssh key公钥内容（id_rsa.pub）

        ```bash
        pbcopy < ~/.ssh/id_rsa.pub
        ```

    5. 配置ssh key公钥内容（id_rsa.pub）到github

        ```bash
        //打开github网站，点击头像，选择Settings
        //选择SSH and GPG keys，点击New SSH key
        //Title随便填，Key填入上面复制的ssh key公钥内容（id_rsa.pub），点击Add SSH key
        ```

    6. 测试ssh key是否配置成功

        ```bash
        //选择SSH and GPG keys，点击New SSH key
        //Title随便填，Key填入上面复制的ssh key公钥内容（id_rsa.pub），点击Add SSH key
        ```

    7. 测试ssh key是否配置成功

        ```bash
        ssh -T git@github.com
        //如果成功，会显示：Hi USERNAME! You
        //如果失败，会显示：Permission denied (publickey).
        ```

## git使用

1. 初始化仓库
    1. 本地初始化仓库

        ```bash
        git init
        ```

    2. 本地初始化仓库并关联远程仓库

        ```bash
        git init
        //如果失败，会显示：Permission denied (publickey).
        ```

2. 查看仓库状态
    ```bash
    git status
    ```
3. 添加文件到暂存区
    ```bash
    git add .
    ```
4. 提交暂存区到本地仓库
    ```bash
    git commit -m "COMMIT_MESSAGE"
    ```
5. 推送本地仓库到远程仓库
    ```bash
    git push origin master
    ```
6. 拉取远程仓库到本地仓库
    ```bash
    git pull origin master
    ```
7. 查看远程仓库
    ```bash
    git remote -v
    ```
8. 查看分支
    ```bash
    git branch
    ```
9.  创建分支
    ```bash
    git branch BRANCH_NAME
    ```
10. 切换分支
    ```bash
    git checkout BRANCH_NAME
    ```
11. 合并分支
    ```bash
    git merge BRANCH_NAME
    ```
12. 删除分支
    ```bash
    git branch -d BRANCH_NAME
    ```
13. 查看提交记录
    ```bash
    git log
    ```
14. 查看提交记录（带图形化）
    ```bash
    git log --graph --pretty=oneline --abbrev-commit
    ```
15. 回退到上一个版本
    ```bash
    git reset --hard HEAD^
    ```
16. 回退到指定版本
    ```bash
    git reset --hard COMMIT_ID
    ```
17. 查看差异
    ```bash
    git diff
    ```
18. 查看差异（带图形化）
    ```bash
    git difftool
    ```
