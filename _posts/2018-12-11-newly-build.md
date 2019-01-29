---
layout: post
author: chao
title: 创建jekyll
---
windows下安装这个玩意

## Setup
以**windows**为例
1. [install ruby](https://rubyinstaller.org/downloads/) 下载最新版本包含devkit的包,然后一路next
2. 安装**jekyll**,命令行中执行:  ```gem install jekyll bundler```
3. 查看版本 ```jekyll -v```
4. 新建一个文件夹,也可以是你的**github.io**的**repo**,在其根目录下创建一个**index.html**文件

index.html
```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Home</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```
5. 此时就可以执行 ```jekyll build```
```
PS C:\_workarea\codes\TakeEasyBoy.github.io> jekyll build
Configuration file: none
            Source: C:/_workarea/codes/TakeEasyBoy.github.io
       Destination: C:/_workarea/codes/TakeEasyBoy.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.089 seconds.
```
6. 浏览器中查看 ```jekyll serve``` 浏览器中打开 ```localhost:4000```

## Liquid
1. Objects 使用双括号 {{ page.title }}
2. Tags 包含if for ``````
3. Filters  ```{{ "hi" | capitalize }}``` 首字母大写

## Front Matter
Front Matter 实际上就是一个包含在了两个 ```---```之间的 yaml的片段,
```
---
my_number: 5
---
```
页面调用
```
{{ page.my_number }}
```
把之前的**index.html**做如下改造,然后看下浏览器变化
```
---
title: Home
---
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World!" | downcase }}</h1>
  </body>
</html>
```
## Includes
## Data Files
## Assete
## Blogging
## Collections
## Deployment