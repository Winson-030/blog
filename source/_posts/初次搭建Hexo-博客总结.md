---
title: 初次搭建Hexo 博客总结
date: 2022-08-20 11:33:49
tags: Hexo 总结
---

# 认识 Hexo

2022年8月，看到朋友搭建了Hexo 博客，看着很有意思。我也想搭一个，写一写记录什么的。搭建的过程中踩了不少坑，下面是初步搭建的记录。

1. 安装`node.js`

   我的操作系统是 `Manjaro Linux`，在终端输入 

   ```shell
   sudo pacman -S community/nodejs-lts-gallium
   ```

   就能成功安装，`nodejs` 自带`npm` 包管理器，是搭建 `Hexo` 博客必备的工具。

   Windows 和 Mac 系统如何安装 nodejs？ 如果你熟悉终端操作，非常推荐使用包管理器在终端下安装！Windows 下用 scoop，Mac 下用 Homebrew。当然直接下载nodejs 安装包也是可以的。

   [Windows 包管理器 scoop 官网](https://scoop.sh/#/)

   [MacOS 包管理器 Homebrew 官网](https://brew.sh/)

   [nodejs 官网](https://nodejs.org/en/download/)

   [菜鸟教程的nodejs 安装指北](https://www.runoob.com/nodejs/nodejs-install-setup.html)

2. npm 安装 `hexo-cli` 

   以下命令都在终端下操作

   1.  查看`nodejs`版本

      ```shell
      ❯ node -v
       v16.16.0
      ```

   2. 查看`npm`版本

      ```shell
      ❯ npm -v
       8.11.0
      ```

   3. 使用`npm`全局安装 `hexo-cli`

      ```shell
      ❯ npm install -g hexo-cli
      ```

   

3. 进入你计划存放 Hexo博客文件夹的目录

   ```shell
   ❯ cd ~/path/you/want/to/save
   ```

   

4. 初始化一个 Hexo 博客

   ```shell
   ❯ hexo init myHexo
   
   INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
   INFO  Install dependencies
   warning hexo-renderer-stylus > stylus > css > source-map-resolve@0.6.0: See https://github.com/lydell/source-map-resolve#deprecated
   INFO  Start blogging with Hexo!
   ```

   

5.  查看初始化的博客文件夹目录

   ```shell
   ❯ ls
   _config.landscape.yml  node_modules  scaffolds  themes
   _config.yml            package.json  source     yarn.lock
   ```

   初次使用，我们需要了解的文件和目录：

   - _config.yml 全局配置Hexo 博客的文件，使用yaml语法，配置时需要谨慎。

   - source 是存放博客文章的目录，文章都存在该目录下的post子目录
   - themes 是存放博客主题的目录

6. 预览初始化后的博客

   初始化后的博客已经可以预览页面了，但比较简陋。自带的主题是`landscape`，可以自己更换主题和插件。在终端输入`hexo s`命令，在浏览器访问`http://localhost:4000/`即可预览，在终端按`Ctrl + c`即可取消预览。

   ```shell
   ❯ hexo s
   INFO  Validating config
   INFO  Start processing
   INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
   ```

   hexo 原始页面

   ![hexo预览图](/images/image-hexo.png)

   

   到这里，hexo博客就成功搭建起来了，但是目前非常简陋，而且只在本地。我会在下一篇记录中分享如何写文章，更换主题，以及部署到Github 上~





