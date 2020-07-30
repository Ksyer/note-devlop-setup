# web开发环境搭建 Linux发行版 deepin v20

- [web开发环境搭建 Linux发行版 deepin v20](#web开发环境搭建-linux发行版-deepin-v20)
  - [01 VS Code](#01-vs-code)
  - [02 git](#02-git)
  - [03 node.js](#03-nodejs)
  - [04 谷歌浏览器](#04-谷歌浏览器)
  - [05 Vue.js脚手架](#05-vuejs脚手架)
  - [06 MySQL及可视化界面工具安装](#06-mysql及可视化界面工具安装)

---

## 01 VS Code

1. 插件安装清单

   - (1). Chinese (Simplified) Language Pack for Visual Studio Code
   - (2). Live Server
   - (3). Markdown All in One
   - (4). markdownlint
   - (5). open in browser
   - (6). Markdown Preview Enhanced
   - (7). vscode-icons

1. 默认浏览器设置

   - (1). 设置 -> 输入 `open in browser` -> chrome

    ![01-01](img/01-01.png)

   - (2). 设置 -> 输入`Liver Server` -> 选择chrome

    ![01-02](img/01-02.png)

## 02 git

1. 安装

   - (1). 操作: `ctrl + alt + t`打开命令行终端, 输入`sudo apt install git`
   - (2). 查询git版本,验证是否安装成功:`git --version`

## 03 node.js

1. 安装

   - (1). 准备: 官网下载nodejs包[注意: 是.tar.g后缀编译后的文件包, 不要下载源码包, 并且对应系统版本, 我的是64-bit]
   - (2). 原理: 简单说就是解压后, 在bin文件夹中已经存在node以及npm, 如果你进入到对应文件的中执行命令行一点问题都没有, 不过不是全局的, 所以将这个设置为全局就好了.
   - (3). 操作: 终端命令行输入:

    ```cmd
    # 在当前压缩包下打开命令行终端操作
    tar -xvf node-v14.5.0-linux-x64.tar.xz
    mv node-v14.5.0-linux-x64 /home/kainan/app/software/
    cd /home/kainan/app/software/node-v0.10.28-linux-x64/bin
    ls
    ./node -v
    ```

    这就妥妥的了，node文件夹具体放在哪，叫什么名字随你怎么定。然后设置全局：

    ```cmd
    mv /home/kainan/app/software/node-v0.10.28-linux-x64 nodejs
    sudo ln -s /home/kainan/app/software/nodejs/bin/npm /usr/local/bin/
    sudo ln -s /home/kainan/app/software/nodejs/bin/node /usr/local/bin/
    ```

    这里/home/kainan/sofltware/这个路径是你自己放的, 你将node文件解压到哪里就是哪里.

2. npm指令

   - (1). `npm list -g --depth 0`, 查看已全局安装的模块  
   - (2). 修改npm镜像地址:
     - a. 命令行:`npm install -g nrm`
     - b. 配置全局的软连接: 相当于win的系统环境变量路径配置

        ```shell
        sudo ln -s /home/kainan/app/software/nodejs/bin/nrm /usr/local/bin/
        ```

## 04 谷歌浏览器

1. 浏览器安装: `sudo apt install chrome`

2. 插件安装清单:
   插件下载网址: <https://www.extfans.com/>
   - (1). Charset: 解决加载的网页乱码问题.
   - (2). 书签侧边栏: 整理收藏网站的资料.

## 05 Vue.js脚手架

1. 安装vue-cli脚手架

   - (1). `npm install -g @vue/cli`
   - (2).  配置全局软连接:

        ```shell
        sudo ln -s /home/kainan/app/software/nodejs/bin/vue /usr/local/bin/
        ```

   - (3). 运行项目所需指令: `npm run serve`

## 06 MySQL及可视化界面工具安装

> 说明: 都是免费开源的工具软件包, 不需要激活或破解, 而且是最新稳定版.

1. MySQL数据库服务端安装

   - (1). 官网下载`mysql-server`的官方仓库. [https://dev.mysql.com/downloads/](https://dev.mysql.com/downloads/)
      说明: 根据自己Linux发行版下载对应的仓库

   - (2).在线安装, 直接参考官方文档进行操作即可. [https://dev.mysql.com/doc/refman/8.0/en/linux-installation.html](https://dev.mysql.com/doc/refman/8.0/en/linux-installation.html)
      说明; 小白不建议二进制包离线安装, 会出很多安装BUG, 大神可随喜好安装

2. 可视化界面工具DBeaver安装

   - (1). 官网下载可安装的文件(installer). [https://dbeaver.io/download/](https://dbeaver.io/download/)
      说明: 并不是下载已经过编译的二进制文件压缩包xxx.zip

   - (2). 根据自己Linux发行版输入相应的安装指令, 我的是基于debain的发行版Linux, 对应输入: `dpkg -i dbeaver-ce_7.1.3_amd64.deb`即可

   - (3). 如果MySQL安装的是8.0以上的版本, 则对应下载`mysql-connector-java-8.0.xx.jar`, 添加到DBeaver中.
      - wyh:
         - a. 因为连接mysql 出现：`java.sql.SQLException: Unable to load authentication plugin 'caching_sha2_password'.` 报错
         - b. mysql-server -> 5.x版本是：default_authentication_plugin=mysql_native_password
         - c.  mysql-server -> 8.x版本就是：default_authentication_plugin=caching_sha2_password
      - other(不推荐):
         - 当然, 也可以从MySQL思考分析, `mysql_native_password`形式下修改密码, 登录MySQL, 输入以下指令即可.(password换成相应密码)

         ```shell
         ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;
         ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
         FLUSH PRIVILEGES;
         alter user 'root'@'localhost' identified by 'password';
         ```

         - 这里有个坑需要注意, 一定看好自己的root用户对应的地址, 默认是localhost, 我之前小组需要改成了%, 这里运行 `ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;`时一直报错, 后来改成`ALTER USER 'root'@'%' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;` 成功运行。
         - 改完加密规则成功运行，后来又发现，在改完加密规则之后，就算MySQL驱动jar包仍然是5.1也可以使用
